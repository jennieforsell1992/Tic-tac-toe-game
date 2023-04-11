<script setup lang="ts">
import InsertUser from "./InsertUser.vue";
import TickTacToe from "./TickTacToe.vue";
import { ref } from "vue";
import { User } from "../models/User";


const user = ref<User[]>([])
const showGame = ref(false)
const currentPlayer = ref(Boolean)

const addPlayerToGame = (userX: User, userO: User) => {
    user.value.push(userX, userO);
    console.log(user)
    showGame.value = true;
}

const ticTacToeBox = () => {

}



</script>

<template>
    <InsertUser :startPage="showGame" @add-username-to-list="addPlayerToGame"></InsertUser>
    <TickTacToe @clicked-box="ticTacToeBox" v-if="showGame"></TickTacToe>
</template>

<style scoped></style>