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

        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],

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
            return boardGame.value[a];



        }

    }

    return null;
}

const winner = computed(() => winnerOfTicTacToe())







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

    if (haswinner === currentPlayer.role) {
        ticTacToeStops();
    }

}

const ticTacToeStops = () => {
    console.log("nu kan jag inte använda spelet mer!")


}

const playAgain = () => {


}




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
    <p v-if="winner === 'X'">winner is: {{ users[0].username }}🎉</p>
    <p v-else> winner is: {{ users[1].username }} </p>
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