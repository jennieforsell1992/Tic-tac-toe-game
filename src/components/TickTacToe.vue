<script setup lang="ts">
import { ref } from "vue";
import { User } from "../models/User";
import { computed } from "@vue/reactivity";


interface ITicTacToeProps {
    users: User[];
}

const props = defineProps<ITicTacToeProps>()
const gameState = ref("start")
const boardKey = ref(0)


let currentPlayer = props.users[0]


let boardGame = ref(["", "", "", "", "", "", "", "", ""])

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
            if (boardGame.value[a] === currentPlayer.role) {
                gameState.value = "win";
                return boardGame.value[a];

            }




        }

    }

    return null;
}

const winner = computed(() => winnerOfTicTacToe())
const newWinner = winner.value;
console.log(newWinner)




const clickedBox = (i: number) => {
    console.log(currentPlayer)
    if (gameState.value != "start") {
        return;
    }


    boardGame.value[i] = currentPlayer.role
    let haswinner = winnerOfTicTacToe();
    console.log(haswinner)

    if (currentPlayer === props.users[0]) {
        currentPlayer = props.users[1];
        console.log(currentPlayer);

    }
    else {
        currentPlayer = props.users[0]
        console.log(currentPlayer)
    }


}



const playAgain = () => {

    for (let i = 0; i < boardGame.value.length; i++) {
        boardGame.value[i] = "";

    }
    gameState.value = "start";
    boardKey.value++;

}




</script>

<template>
    <p class="usernameX" v-if="currentPlayer.role === 'X'"> Player {{ users[0].username }} 's turn:</p>
    <p class="usernameO" v-else> Player {{ users[1].username }} 's turn:</p>
    <div div class=" square-container">
        <div class="square" v-for="(square, index) in boardGame" :key="boardKey" @click.once="() => { clickedBox(index) }">
            {{
                boardGame[index] }}
        </div>
    </div>
    <div class="btn-container">
        <button class="reset-btn" @click="playAgain">Reset game</button>
    </div>
    <div class="winner-container">
        <p class="usernameWinnerO" v-if="gameState === 'win' && currentPlayer.role === 'X'">winner is: {{ users[1].username
        }}🎉
        </p>
        <p class="usernameWinnerX" v-if="gameState === 'win' && currentPlayer.role === 'O'">winner is: {{ users[0].username
        }}🎉
        </p>
    </div>
</template>

<style scoped>
.usernameX {
    color: white;
}

.usernameO {
    color: white;
}

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
    background-color: pink;

}

.square:hover {
    background-color: lightpink;
}

.btn-container {
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;

}

.reset-btn {
    background-color: pink;

}

.reset-btn:hover {
    background-color: white;
    border-color: white;
}

.winner-container {

    display: flex;
    justify-content: center;
    align-items: center;
}

.usernameWinnerO {
    color: white;

}

.usernameWinnerX {

    color: white;
}
</style>