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
    <form class="form" :class="{ hidden: startPage }">
        <label class="labelX">Player X</label>
        <input class="playerX" type="text" placeholder="Name" v-model="userX.username">
        <label class="labelO">Player O</label>
        <input class="playerO" type="text" placeholder="Name" v-model="userO.username">
        <button class="player-btn" @click.prevent="handleClick">save</button>
    </form>
</template>

<style scoped>
.form {
    margin: 50px;
    padding: 50px;
    display: flex;
    flex-direction: column;
    background-color: pink;
    border-radius: 5px;
}

.labelX {
    font-size: 1.4rem;

}

.labelO {
    font-size: 1.4rem;
    margin-top: 10%;
}

.playerX {
    border-radius: 8px;
    padding: 5px;

}

.playerO {
    border-radius: 8px;
    padding: 5px;
}

.player-btn {
    margin-top: 20%;
    border-color: #242424;
    background-color: white;
}

.player-btn:hover {

    background-color: #ffb6c1;
    border-color: white;
}





.hidden {
    display: none;
}
</style>