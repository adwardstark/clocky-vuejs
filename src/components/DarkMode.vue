<script setup lang="ts">
import { ref } from 'vue';

const isInDarkMode = ref(localStorage.getItem('dark-mode') === 'true');

if(isInDarkMode.value) {
  document.querySelector('html')?.classList.add('dark');
}

const toggleDarkMode = () => {
  const html = document.querySelector('html');
  if (isInDarkMode.value) {
    html?.classList.remove('dark');
  } else {
    html?.classList.add('dark');
  }

  isInDarkMode.value = !isInDarkMode.value;
  localStorage.setItem('dark-mode', isInDarkMode.value.toString());
};
</script>

<template>
    <div class="fab ripple" @click="toggleDarkMode">
      <i class="fas icon" :class="[isInDarkMode ? 'fa-sun' : 'fa-moon']"></i>
    </div>
</template>