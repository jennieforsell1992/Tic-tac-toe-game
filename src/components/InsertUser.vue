<script setup lang="ts">
import { ref } from "vue";

const usernameOne = ref("")
const usernameTwo = ref("")

</script>

<template>
    <form>
        <input type="text" placeholder="Player one" v-model="usernameOne">
        <input type="text" placeholder="Player two" v-model="usernameTwo">
        <button>save</button>
    </form>
    {{ usernameOne }}
    {{ usernameTwo }}
</template>

<style scoped></style>