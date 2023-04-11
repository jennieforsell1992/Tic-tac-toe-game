<script setup lang="ts">
import { ref } from "vue";
import { User } from "../models/User";

interface ITicTacToeProps {
    users: User[];
}
const props = defineProps<ITicTacToeProps>()

let currentPlayer = props.users[0]


const boardGame = ref([{ clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" },])





const clickedBox = (i: number) => {
    console.log(currentPlayer)

    boardGame.value[i].symbol = currentPlayer.role
    boardGame.value[i].clicked = true;
    if (currentPlayer === props.users[0]) {
        currentPlayer = props.users[1];

    }
    else {
        currentPlayer = props.users[0]
    }


    console.log("klickade på rutan", i)
    console.log(boardGame.value[i])

}



</script>

<template>
    <p></p>
    <div class="square-container">
        <div class="square" v-for="(square, index) in boardGame" :key="index" @click.once="() => { clickedBox(index) }">{{
            boardGame[index].symbol }}
        </div>
    </div>
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