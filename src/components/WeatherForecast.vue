<script setup>
defineProps({
    day:Object
})
</script>
<template>
    <main class="mb-2 hover:scale-105 scale-90 transition cursor-pointer flex items-center justify-between rounded-lg bg-gray-400/40 shadow-lg px-3 py-2">
        
        <div class="p-2 lg:flex flex-col lg:items-center gap-4">
            <p class="lg:text-2xl font-light">{{ Math.round(day.day.avgtemp_c) }} &deg;C</p>
            <div>
                <img :src="day.day.condition.icon" width="30" class="mx-auto lg:w-28" alt="">
            </div>
            <p class="text-lg tracking-widest">
                {{ new Date(day.date).toLocaleDateString('eu-us',{weekday:'short'}) }}
            </p>
        </div>
    </main>
</template>