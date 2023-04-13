<script setup lang="ts">
import { ref, computed } from "vue";
import { User } from "../models/User";


interface ITicTacToeProps {
    users: User[];
}

const props = defineProps<ITicTacToeProps>()


let currentPlayer = props.users[0]


const boardGame = ref(["", "", "", "", "", "", "", "", ""])

const winnerOfTicTacToe = () => {
    const winCondition = [

        [0, 1, 2], // 0
        [3, 4, 5],  // 1
        [6, 7, 8],  // 2

        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],

        [0, 4, 8],
        [2, 4, 6],
    ]


    for (let i = 0; i < winCondition.length; i++) {
        const winners = winCondition[i];
        const [a, b, c] = winners;

        if (boardGame.value[a] && boardGame.value[a] === boardGame.value[b] && boardGame.value[a] === boardGame.value[c]) {
            return true;


        }



        //     console.log(winners)

        //     for (let j = 0; j < winners.length; j++) {
        //         const positionInList = winners[j];
        //         console.log(boardGame.value[positionInList])

        //         if (boardGame.value[positionInList] === player) {


        //         }


        //     }



        // }
    }

    return false;
}

const winner = computed(() => winnerOfTicTacToe())


// https://github.com/TylerPottsDev/yt-vue-tictactoe/blob/master/src/App.vue




const clickedBox = (i: number) => {
    console.log(currentPlayer)


    boardGame.value[i] = currentPlayer.role
    let haswinner = winnerOfTicTacToe();

    if (currentPlayer === props.users[0]) {
        currentPlayer = props.users[1];

    }
    else {
        currentPlayer = props.users[0]
    }


    console.log("klickade på rutan", i)
    console.log(boardGame.value[i])

    if (haswinner === true) {
        ticTacToeStops();
    }

}

const ticTacToeStops = () => {
    console.log("nu kan jag inte använda spelet mer!")


}

const playAgain = () => {


}


// const resetGame = () => {

//     boardGame.value = ["", "", "", "", "", "", "", "", ""]

// }



</script>

<template>
    <p v-if="currentPlayer.role === 'X'"> Player {{ users[0].username }} 's turn:</p>
    <p v-else> Player {{ users[1].username }} 's turn:</p>
    <div div class=" square-container">
        <div class="square" v-for="(square, index) in boardGame" :key="index" @click.once="() => { clickedBox(index) }">{{
            boardGame[index] }}
        </div>
    </div>
    <button>Reset game</button>
    <p>winner is: {{ winner }}</p>
</template>

<style scoped>
.square-container {

    margin: 0 auto;
    display: grid;
    grid-template-columns: 33% 33% 33%;
    grid-template-rows: 33% 33% 33%;
    max-width: 300px;
}

.square {
    border: 1px solid white;
    min-width: 100px;
    min-height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 50px;
    cursor: pointer;
    background-color: deeppink;

}

.square:hover {
    background-color: #242424;
}
</style>