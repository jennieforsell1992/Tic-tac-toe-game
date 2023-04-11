<script setup lang="ts">
import InsertUser from "./InsertUser.vue";
import TickTacToe from "./TickTacToe.vue";
import { ref } from "vue";
import { User } from "../models/User";

const user = ref<User[]>([])

</script>

<template>
    <InsertUser></InsertUser>
    <TickTacToe></TickTacToe>
</template>

<style scoped></style>