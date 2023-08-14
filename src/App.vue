<script setup>
import Carousel from './components/Carousel.vue';
import PieChart from './components/PieChart.vue';
import { ref } from 'vue'
let task = ref(1) // 1 for Carousel's visibility and 2 for PieChart's visibility
</script>

<template>
  <div class="mx-auto container my-10 text-center">
    <h1 class="text-3xl text-slate-700 mt-10">An Assignment on Vue LifeCycle Hooks</h1>
    <p class="text-slate-500 mt-2 mb-10">Clean up message will show in console</p>
    <button @click="task = 1" :class="1==task?'bg-blue-700': 'bg-blue-400'" class="mr-4 mb-20 text-2xl rounded py-2 px-10 text-white hover:bg-blue-500">Carousel</button>
    <button @click="task = 2" :class="2==task?'bg-blue-700': 'bg-blue-400'" class="mb-20 text-2xl rounded py-2 px-10 text-white hover:bg-blue-500">Chart</button>
    <Carousel v-if="1 === task" />
    <PieChart v-if="2 === task" />
  </div>
</template>

<style scoped></style>
