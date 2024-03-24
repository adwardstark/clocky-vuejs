<script setup lang="ts">
import { ref, type CSSProperties } from 'vue';
import DarkMode from './components/DarkMode.vue';

const currentTime = ref('');
const currentDate = ref('');

const hrStyle = ref({ transform: 'translate(-50%, -100%) rotate(0deg)' } as CSSProperties);
const minStyle = ref({ transform: 'translate(-50%, -100%) rotate(0deg)' } as CSSProperties);
const secStyle = ref({ transform: 'translate(-50%, -100%) rotate(0deg)' } as CSSProperties);

const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

// StackOverflow https://stackoverflow.com/questions/10756313/javascript-jquery-map-a-range-of-numbers-to-another-range-of-numbers
const scale = (num: number, in_min: number, in_max: number, out_min: number, out_max: number) => {
    return (num - in_min) * (out_max - out_min) / (in_max - in_min) + out_min;
}

const setTime = () => {
    const time = new Date();
    const month = time.getMonth()
    const day = time.getDay()
    const date = time.getDate()
    const hours = time.getHours()
    const hoursForClock = hours >= 13 ? hours % 12 : hours;
    const minutes = time.getMinutes()
    const seconds = time.getSeconds()
    const ampm = hours >= 12 ? 'PM' : 'AM'

    hrStyle.value = { transform: `translate(-50%, -100%) rotate(${scale(hoursForClock, 0, 12, 0, 360)}deg)` }
    minStyle.value = { transform: `translate(-50%, -100%) rotate(${scale(minutes, 0, 60, 0, 360)}deg)` }
    secStyle.value = { transform: `translate(-50%, -100%) rotate(${scale(seconds, 0, 60, 0, 360)}deg)` }

    currentTime.value = `${hoursForClock}:${minutes < 10 ? `0${minutes}` : minutes} ${ampm}`
    currentDate.value = `${days[day]}, ${months[month]} ${date}`
}

setTime()

setInterval(setTime, 1000)
</script>

<template>
    <div class="clock-container">
      <div class="clock">
        <div class="needle hour" :style="hrStyle"></div>
        <div class="needle minute" :style="minStyle"></div>
        <div class="needle second" :style="secStyle"></div>
        <div class="center-point"></div>
      </div>

      <div class="time">{{ currentTime }}</div>
      <div class="date">{{ currentDate }}</div>
    </div>

    <DarkMode />
</template>

<style scoped>

</style>
