<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';
let carousel = null;
const images = ref([
    "https://images.unsplash.com/photo-1690200371742-128cb94657df?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
    "https://images.unsplash.com/photo-1691735032448-4379424fbb32?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=960&q=80",
    "https://images.unsplash.com/photo-1682695796954-bad0d0f59ff1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=960&q=80",
    "https://images.unsplash.com/photo-1691315391544-ec0aa2d54a9e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1176&q=80"
])
let newImage = ref("https://images.unsplash.com/photo-1682685797366-715d29e33f9d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80")

function startCarousel() {
    carousel = new Flickity('#carousel', {
        wrapAround: true,
        autoPlay: 1500,
        pauseAutoPlayOnHover: true
    });
}

function addNewImage() {
    images.value.push(newImage.value)
    carousel.destroy()
    nextTick(() => {
        startCarousel()
    })
}
onBeforeUnmount(() => {
    carousel.destroy()
    console.log("All Slider data is Unmounted and ongoing task is cleaned up");
})
onMounted(() => {
    startCarousel()
})
</script>

<template>
    <h1 class="text-2xl text-slate-700 mb-4">Carousel - Total Images({{ images.length }})</h1>
    <input type="url" v-model="newImage" placeholder="Image Url">
    <button @click="addNewImage()"
        class="py-2 px-4 ml-2 rounded border-blue-500 border-2 text-white bg-blue-400 hover:bg-blue-500">
        Add Image
    </button>

    <div id="carousel" class="mx-auto text-center mt-10">
        <div class="single-img text-orange-500" v-for="(image, index) in images" :key="index"
            :style="`background-image: url(${image}); background-position: center center; background-size: 100%; background-repeat: no-repeat`">
        </div>
    </div>
</template>

<style scoped>
input {
    border: 1px solid #aaa;
    padding: 10px 20px;
    border-radius: 5px;
    width: 300px;
}

#carousel {
    width: 420px;
}

.single-img {
    width: 420px;
    height: 300px;
}
</style>