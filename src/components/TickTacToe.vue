<script setup lang="ts">
import { ref } from "vue";
import { User } from "../models/User";

interface ITicTacToeProps {
    users: User[];
}
const props = defineProps<ITicTacToeProps>()

const currentPlayer = props.users[0]


const boardGame = ref([{ clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" }, { clicked: false, symbol: "" },])

const emit = defineEmits(["clickedBox"])



const clickedBox = (index: number) => {
    if (currentPlayer.role === "X") {
        boardGame.value[index].symbol = currentPlayer.role
    }
    else (currentPlayer.role === "O"); {
        boardGame.value[index].symbol = currentPlayer.role
    }

    console.log("klickade på rutan", index)
    console.log(boardGame.value[index])

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