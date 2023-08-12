<script setup>
import { ref, reactive, onMounted, nextTick } from 'vue'

const items = [
    'https://images.unsplash.com/photo-1682687982046-e5e46906bc6e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
    'https://images.unsplash.com/photo-1682686581498-5e85c7228119?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
    'https://images.unsplash.com/photo-1682687982167-d7fb3ed8541d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=871&q=80'
]

let carousel = null

onMounted(() =>{
    carousel = new Flickity( '#carousel', {});
})

let newItem = ref('')

function updateCarousel(){
    items.push(newItem.value)
    console.log(items)
    carousel.destroy()

    nextTick(() =>{
        carousel = new Flickity( '#carousel', {});
    })
}

</script>
<template>
    <form>
        <div class="grid gap-6 mb-6 md:grid-cols-2">
        <div>
            <input v-model="newItem" type="text" id="color-name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Image URL">
        </div>
        <div>
            <button @click.prevent="updateCarousel()" type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add to Carousel</button>
        </div>        
        </div>
    </form>
    <div class="mx-auto items" id="carousel">
        <div class="item" :style="`background-image:url(${item})`" v-for="(item, index) in items" :key="index">{{ index+1 }}</div>
    </div>    
</template>

<style scoped>
.items{
    width: 800px;
    height:400px;
}

.item{
    width: 800px;
    height: 400px;
    background-color: gray;
    background-size: cover;
}
</style>
