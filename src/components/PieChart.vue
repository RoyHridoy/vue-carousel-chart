<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
let itemValue = ref(6500)
let itemName = ref('Groceries')
let color = ref('#00c331')
let dataset = [500, 1400, 1080, 5000]
let labels = ["water", "electricity", "gas", "rent"]
let bgColor = ['rgb(255, 99, 132)', 'rgb(54, 162, 235)', 'rgb(255, 205, 86)', '#681062']
let pieChart = null

const data = {
    labels: labels,
    datasets: [{
        label: ' Expenditure',
        data: dataset,
        backgroundColor: bgColor,
        hoverOffset: 4
    }]
};

const config = {
    type: 'pie',
    data: data,
};

function addNewItem() {
    labels.push(itemName.value)
    bgColor.push(color.value)
    dataset.push(itemValue.value)
    pieChart.destroy()
    nextTick(() => {
        const element = document.getElementById('pieChart')
        pieChart = new Chart(element, config)
    })
}

onMounted(() => {
    const element = document.getElementById('pieChart')
    pieChart = new Chart(element, config);
})

</script>

<template>
    <h1 class="text-2xl text-slate-700 mb-4">Expenditure</h1>
    <div class="bg-slate-300 py-20 w-full sm:w-1/2 mx-auto">
        <canvas id="pieChart"></canvas>
    </div>
    <div class="mx-auto mt-10 pb-40 input-data text-left">
        <label for="title" class="mb-1 block">Item Title</label>
        <input type="text" v-model="itemName" placeholder="Title" id="title">
        <label for="value" class="mb-1 block">Item value</label>
        <input type="number" v-model="itemValue" placeholder="Value">
        <label for="color" class="mb-1 block">Choose Color</label>
        <input type="color" v-model="color" id="color">
        <button @click="addNewItem()"
            class="py-2 px-4 mt-4 rounded border-blue-500 border-2 text-white bg-blue-400 hover:bg-blue-500" type="submit">
            Add Item
        </button>
    </div>
</template>

<style scoped>
input {
    border: 1px solid #aaa;
    padding: 10px 20px;
    border-radius: 5px;
    width: 300px;
    display: block;
    margin-bottom: 20px;
}

#pieChart {
    max-width: 400px;
    margin: 0 auto;
}

.input-data {
    max-width: 400px;
}
</style>
