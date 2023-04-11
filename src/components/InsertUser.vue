<script setup lang="ts">
import { ref } from "vue";
import { User } from "../models/User";

const userX = ref<User>({ username: "", role: "X" })
const userO = ref<User>({ username: "", role: "O" })


const emit = defineEmits(["addUsernameToList"])

const handleClick = () => {
    emit("addUsernameToList", userX.value, userO.value)

}

</script>

<template>
    <form>
        <input type="text" placeholder="Player one" v-model="userX.username">
        <input type="text" placeholder="Player two" v-model="userO.username">
        <button @click.prevent="handleClick">save</button>
    </form>
    {{ userX }}
    {{ userO }}
</template>

<style scoped></style>