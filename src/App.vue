<script setup>
import Search from './components/Search.vue';
import WeatherCard from './components/WeatherCard.vue';
import { ref } from 'vue';
const places = ref([]);

const addPlace = (data) => {
  places.value.push(data)
  // console.log(data );
}
const deletePlace = (name) => {
  places.value = places.value.filter(place=> place.location.name !== name)
  // console.log(name);
}
</script>

<template>
  <main class="py-4">
    <div class="text-right  pt-2 mb-6 pr-5 tracking-wider ">
    <span class=" text-sm text-white">
      {{ new Date().toLocaleDateString('eu-us', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
      }) }}
    </span>
    </div>
    <div>
      <Search @place-data="addPlace" />
    </div>
    <div v-for="(place,index) in places" :key="index">
      <WeatherCard :place="place" @delete-place="deletePlace" />
    </div>
  </main>
</template>

