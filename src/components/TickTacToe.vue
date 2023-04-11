<script setup lang="ts">


const boardGame = [1, 2, 3, 4, 5, 6, 7, 8, 9]

const emit = defineEmits(["clickedBox"])

const clickedBox = (index: number) => {
    emit("clickedBox", index)
}



</script>

<template>
    <div class="square-container">
        <div class="square" v-for="(square, index) in boardGame" :key="index" @click.once="() => { clickedBox(index) }"></div>
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