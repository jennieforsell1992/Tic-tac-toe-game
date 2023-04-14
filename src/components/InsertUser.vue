<script setup lang="ts">
import { ref } from "vue";
import { User } from "../models/User";

const userX = ref<User>({ username: "", role: "X" })
const userO = ref<User>({ username: "", role: "O" })

interface IShowStartPage {
    startPage: boolean;
}

defineProps<IShowStartPage>()


const emit = defineEmits(["addUsernameToList"])

const handleClick = () => {
    emit("addUsernameToList", userX.value, userO.value)

}

</script>

<template>
    <form :class="{ hidden: startPage }">
        <input type="text" placeholder="Player one" v-model="userX.username">
        <input type="text" placeholder="Player two" v-model="userO.username">
        <button @click.prevent="handleClick">save</button>
    </form>
</template>

<style scoped>
.hidden {
    display: none;
}
</style>