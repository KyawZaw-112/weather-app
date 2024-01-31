<script setup>
import BorderLine from './BorderLine.vue';
defineProps({
    place: Object,
})
</script>

<template>
    <div class="absolute bg-white/30 z-10 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8">
        <!-- Close button -->
        <div class="flex justify-end lg:justify-between lg:items-center mb-10 lg:mb-20">
            <h1 class="lg:text-xl text-white lg:visible  invisible tracking-wider font-semibold ">More Information</h1>
            <button class="p-1 hover:scale-100 scale-90 transition active:scale-75" @click="$emit('close-detail')">
                <i class="fa-solid fa-xmark text-xl lg:text-3xl"></i>
            </button>
        </div>
        <div class="lg:flex lg:item-center gap-5 text-slate-800/80">
            <div class="flex items-top justify-between lg:justify-start gap-6 mb-10 ">
                <!-- Wind speed -->
                <div class="text-center flex-1 lg:flex-none lg:gap-5 flex flex-col lg:flex-row items-center">
                    <i class="fa-solid fa-wind mb text-2xl"></i>
                    <p class=" text-xs">wind</p>
                    <p class="text-sm font-bold">{{ place.current.wind_kph }} km/h</p>
                    <p class="hidden lg:block">|</p>
                </div>
                <!-- Humidity level -->
                <div class="text-center flex-1 lg:flex-none lg:gap-5 flex flex-col lg:flex-row items-center">
                    <i class="fa-solid fa-droplet mb text-2xl"></i>
                    <p class=" text-xs">humidity</p>
                    <p class="text-sm font-bold">{{ place.current.humidity }} %</p>
                    <p class="hidden lg:block">|</p>
                </div>
                <!-- Precipitation -->
                <div class="text-center flex- lg:flex-none lg:gap-5 flex flex-col lg:flex-row items-center">
                    <i class="fa-solid fa-umbrella mb text-2xl"></i>
                    <p class=" text-xs">precipitation</p>
                    <p class="text-sm font-bold">{{ place.current.precip_in }} inch</p>
                    <p class="hidden lg:block">|</p>
                </div>
            </div>
            <div class="flex items-center justify-between lg:justify-start gap-6 mb-10">
                <!-- Wind direction -->
                <div class="text-center flex-1 lg:flex-none lg:gap-5 flex flex-col lg:flex-row items-center">
                    <i class="fa-solid fa-fan mb text-2xl"></i>
                    <p class=" text-xs">direction</p>
                    <p class="text-sm font-bold">{{ place.current.wind_dir }}</p>
                    <p class="hidden lg:block">|</p>
                </div>
                <div class="text-center flex-1 lg:flex-none lg:gap-5 flex flex-col lg:flex-row items-center">
                    <i class="fa-solid fa-temperature-half mb text-2xl"></i>
                    <p class=" text-xs">Feel</p>
                    <p class="text-sm font-bold">{{ Math.round(place.current.feelslike_c) }} &deg;C</p>
                    <p class="hidden lg:block">|</p>
                </div>
                <!-- UV -->
                <div class="text-center flex-1 lg:flex-none lg:gap-5 flex flex-col lg:flex-row items-center">
                    <i class="fa-solid fa-sun mb text-2xl"></i>
                    <p class=" text-xs">UV index</p>
                    <p class="text-sm font-bold">{{ place.current.uv }}</p>
                </div>
            </div>
        </div>
        <BorderLine class="hidden lg:block" />
        <div class="hidden lg:flex mt-12 gap-x-7 mb-10">
            <div class="flex items-baseline gap-2">
                <i class="fa-solid fa-sun"></i>
                <p class="text-md font-light">Sun rise</p>
                <p class="text-xl text-slate-800">{{ place.forecast.forecastday[0].astro.sunrise }} |</p>
            </div>
            <div class="flex items-baseline gap-2">
                <i class="fa-solid fa-moon"></i>
                <p class="text-md font-light">Moon rise</p>
                <p class="text-xl text-slate-800">{{ place.forecast.forecastday[0].astro.moonrise }} |</p>
            </div>
            <div class="flex items-baseline gap-2">
                <i class="fa-solid fa-mountain-sun"></i>
                <p class="text-md font-light">Sun set</p>
                <p class="text-xl text-slate-800">{{ place.forecast.forecastday[0].astro.sunset }} |</p>
            </div>
        </div>
        <!-- Last update and delete -->
        <div class="flex justify-between items-center ">
            <h3 class="text-slate-900/50 text-xs lg:text-lg/10">last update: {{ place.current.last_updated }}</h3>
            <button class=" hover:scale-100 scale-90 transition active:scale-75" @click="$emit('remove-place')">
                <i
                    class="fa-solid fa-trash text-rose-600 lg:text-2xl"></i>
            </button>
        </div>
    </div>
</template>