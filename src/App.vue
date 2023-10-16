<template>
  <div class="relative bg-black bg-opacity-30 backdrop-blur-md z-0">
    <AppNavbar/>

    <!-- Landing Content (fullscreen emphasis) -->
    <div class="flex flex-col justify-center min-h-screen relative">
      <div class="text-center space-y-4">
        <p class="text-4xl lg:text-6xl font-light">Join the first ever</p>
        <p class="text-4xl lg:text-6xl font-bold">Bebras Challenge</p>
        <p class="text-4xl lg:text-6xl font-light">in KISJ</p>
        <p class="text-lg lg:text-md font-light">Hosted by Easy Computing Club</p>
      </div>

      <!-- Scroll Down Indicator -->
      <div class="absolute bottom-16 w-full text-center"> <!-- Adjusted this line -->
        <p class="text-white">Scroll Down</p>
        <svg class="w-6 h-10 mx-auto animate-bounce" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
        </svg>
      </div>
    </div>

    <!-- Additional Content Below the Fold -->
    <div class="p-4 lg:p-12 max-w-screen-lg mx-auto space-y-8 mt-8">
      <!-- Bebras Challenge Info -->
      <div v-if="domReady" :style="computeBoxStyle($el)" class="glassmorphic-box space-y-4">
        <p class="text-2xl font-semibold">What is Bebras Challenge?</p>
        <p>The USA Bebras Challenge tests your logic and computational skills through different types of fun and challenging problems.</p>
      </div>

      <!-- Coding Info -->
      <div v-if="domReady" :style="computeBoxStyle($el)" class="glassmorphic-box space-y-4">
        <p class="text-2xl font-semibold">Don't know coding?</p>
        <p>No worries! Bebras Challenge requires no prior knowledge of computer science. All you need is logical thinking and problem-solving skills.</p>
        <p>Sign up now! You don't know what you're missing out on!</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import AppNavbar from "./components/AppNavbar.vue";
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';

const domReady = ref(false);
const mouseX = ref(0);
const mouseY = ref(0);

onMounted(() => {
  nextTick(() => {
    domReady.value = true;
  });
  document.addEventListener('mousemove', handleMouseMove);
});


onBeforeUnmount(() => {
  document.removeEventListener('mousemove', handleMouseMove);
});

function handleMouseMove(event) {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
}

const computeBoxStyle = (element) => {
  const rect = element.getBoundingClientRect();

  const depth = 5;  // Adjust this to change the effect's intensity

  // check window is focused or rseet dx
  if (document.hasFocus()) {
    const dx = (mouseX.value - rect.left - rect.width / 2) / rect.width;
    return {
      transform: `perspective(1000px) rotateY(${dx * depth}deg) rotateX(0deg)`,
      transition: 'transform 0.3s ease-out'
    };
  } else {
    return {
      transform: `perspective(1000px) rotateY(0deg) rotateX(0deg)`,
      transition: 'transform 0.3s ease-out'
    };
  }
}
</script>

<style>
.glassmorphic-box {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  padding: 2rem;
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  will-change: transform;  /* Optimization */
}
</style>
