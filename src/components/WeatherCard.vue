<script setup>
import { ref } from 'vue';
import BorderLine from './BorderLine.vue'
import WeatherForecast from './WeatherForecast.vue';
import WeatherInfo from './WeatherInfo.vue';
defineProps({
    place: Object
});
const showDetail = ref(false)
const emit = defineEmits(['delete-place']);
const removePlace = (placeName) => {
    emit('delete-place', placeName);
    showDetail.value = false
}
</script>
<template>
    <main
    :class="place.current.is_day === 1 ? 'bg-day':'bg-night '"
        class="text-white mx-4  pb-10 pt-10  px-4 lg:px-20 rounded-lg shadow-2xl gap-6 mt-4 mb-6 relative overflow-hidden">
        <section class="flex flex-col gap-4 mb-3">
            <div class="flex justify-between items-center lg:flex-row-reverse">
                <div class="flex gap-4 items-center">
                    <i class="fa-solid fa-location-dot"></i>
                    <h1 class="text-xs lg:text-xl font-light">{{ place.location.name }} , {{ place?.location.country }}</h1>
                </div>
                <img :src="place?.current?.condition?.icon" alt="icon" class="lg:w-[140px]">
            </div>
            <h1 class="text-7xl font-extralight">{{ Math.round(place?.current?.temp_c) }} &deg;C</h1>
            <div class=" flex flex-col gap-4">
                <p class="text-4xl font-light">{{ new Date(place?.location?.localtime).getDate() }} {{ new
                    Date(place?.location?.localtime).toLocaleDateString("eu-us", { month: 'short' }) }} {{ new
        Date(place?.location?.localtime).toLocaleDateString("eu-us", { year: 'numeric' }) }}</p>

                <div class="flex gap-6 *:text-lg *:font-light">
                    <p>
                        {{ new Date(place?.location.localtime).toLocaleDateString("eu-us", { weekday: 'long' }) }}
                    </p>
                    |
                    <p>
                        {{ new Date(place?.location.localtime).getHours() }}:{{ new
                            Date(place?.location.localtime).getMinutes() }}
                    </p>
                </div>
            </div>
        </section>

        <BorderLine class="lg:hidden" />
        <h1 class="mt-5 text-xl tracking-wider">Forecast</h1>
        <div class="flex flex-row flex-wrap lg:justify-start justify-center gap-x-2 lg:gap-x-3 gap-y-2 mt-5">
            <div v-for="(day, index) in place.forecast.forecastday" :key="index">
                <WeatherForecast :day="day" />
            </div>
        </div>
        <Transition name="fade">

            <div v-show="showDetail">
                <WeatherInfo @remove-place="removePlace(place.location.name)" :place="place"
                    @close-detail='showDetail = false' />
            </div>
        </Transition>
        <div class="flex justify-center items-center gap-1 mt-10 px-5 hover:scale-100 scale-90 transition active:scale-75">
            <button @click="showDetail = true">See more information<i
                    class="fa-solid fa-arrow-right text-sm -mb-px ml-4"></i></button>
        </div>
    </main>
</template>
<style scoped>
.fade-enter-active,.fade-leave-active {
    transition: opacity 0.5s ease ;
}
.fade-enter-from,.fade-leave-to{
    opacity: 0;
}
.bg-day {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
}
.bg-night {
  background-color: #07223d;
  background-image: linear-gradient(62deg, #0a2a4a 0%, #270845 70%);
}
</style>