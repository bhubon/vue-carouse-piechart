<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

let chart = null
let newItem = ref(16)

const dataset = [
    300, 50, 100
]

const data = {
    labels: [
        'Red',
        'Blue',
        'Yellow'
    ],
    datasets: [{
        label: 'My First Dataset',
        data: dataset,
        backgroundColor: [
            'rgb(255, 99, 132)',
            'rgb(54, 162, 235)',
            'rgb(255, 205, 86)'
        ],
        hoverOffset: 4
    }]
};


const config = {
    type: 'pie',
    data: data,
};

onMounted(() => {
    const ctx = document.getElementById('chart')
    chart = new Chart(ctx, config);

})

onBeforeUnmount(() => {
    // nothing to do here fot this task
})

function updateChart() {
    dataset.push(newItem.value)
    data.datasets[0].data = dataset
    chart.update()
}

</script>
<template>
    <h2 class="text-3xl mb-5">PieChart</h2>
    <div class=" mx-auto w-[400px] h-[400px] bg-gray-400">
        <canvas id="chart">
        </canvas>
    </div>

    <div class="mt-20">
        <input type="text" v-model="newItem">
        <button @click="updateChart()" class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Add
        </button>

    </div>
</template>

<style lang="scss" scoped></style>