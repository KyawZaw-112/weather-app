<script setup>

import { reactive } from 'vue';

const emit = defineEmits(['place-data'])

const searchTerm = reactive({
    query: '',
    timeout: null,
    results: null
})

const handleSearch = () => {
    clearTimeout(searchTerm.timeout)
    searchTerm.timeout = setTimeout(async () => {
        if (searchTerm.query !== '') {
            // console.log(searchTerm.query);
            const fetchData = await fetch(`http://api.weatherapi.com/v1/search.json?key=7d6a3afe6fec46849b441712242901&q=${searchTerm.query}`)
            const data = await fetchData.json()
            searchTerm.results = data
        } else {
            searchTerm.results = null
        }
    }, 500)
}

const fetchWeather = async(id) => {
    const getForcast = await fetch(`http://api.weatherapi.com/v1/forecast.json?key=7d6a3afe6fec46849b441712242901&q=id:${id}&days=7&aqi=no&alerts=no`) 
    const data =  await getForcast.json();
    emit('place-data',data)
    searchTerm.query = '';
    searchTerm.results = null
}
</script>

<template>
    <section>
        <form>
            <div class=" flex justify-center flex-col items-center gap-4">
                <h1 class=" mb-3 tracking-wider text-white">Expore Country's Weather</h1>
                <div class="bg-white border-indigo-600/30 rounded-lg shadow-md flex items-center w-3/4">
                    <i class=" fa-solid fa-magnifying-glass p-2 text-indigo-600"></i>
                    <input @input="handleSearch" v-model="searchTerm.query" type="text" placeholder="Search" class="rounded-r-lg p-2 border-0 outline-0 focus:ring-2 focus\
                ring-indigo-600 ring-inset w-full">
                </div>
            </div>
        </form>
        <div class="bg-white my-2 rounded-lg shadow-lg w-3/4 mx-auto py-2 px-4"  v-if="searchTerm.results !== null">
            <div v-for="place in searchTerm.results" :key="place.id">
                <button @click="fetchWeather(place.id)" class="px-3 text-xs md:text-xl md:font-medium md:tracking-wider my-2 hover:text-indigo-600 md:hover:font-bold md:hover:scale-105 md:scale-95 transition">
                    {{ place.name }}, {{ place.region }}, {{ place.country }}
                </button>
                <hr/>
            </div>
        </div>
        
    </section>
</template>