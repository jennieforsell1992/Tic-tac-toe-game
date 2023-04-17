<script setup lang="ts">
import InsertUser from "./InsertUser.vue";
import TickTacToe from "./TickTacToe.vue";
import { ref } from "vue";
import { User } from "../models/User";


const user = ref<User[]>([])
const showGame = ref(false)

const addPlayerToGame = (userX: User, userO: User) => {
    user.value.push(userX, userO);
    showGame.value = true;
    console.log(user)
}



</script>

<template>
    <InsertUser :startPage="showGame" @add-username-to-list="addPlayerToGame"></InsertUser>
    <TickTacToe :users="user" v-if="showGame"></TickTacToe>
</template>

<style scoped></style>