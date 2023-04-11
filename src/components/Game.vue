<script setup lang="ts">
import InsertUser from "./InsertUser.vue";
import TickTacToe from "./TickTacToe.vue";
import { ref } from "vue";
import { User } from "../models/User";


const user = ref<User[]>([])

const addPlayerToGame = (userX: User, userO: User) => {
    user.value.push(userX, userO);
    console.log(user)
}

</script>

<template>
    <InsertUser @add-username-to-list="addPlayerToGame"></InsertUser>
    <TickTacToe></TickTacToe>
</template>

<style scoped></style>