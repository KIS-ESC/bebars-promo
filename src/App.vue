<template>
  <div class="relative bg-black bg-opacity-30 backdrop-blur-md z-0">
    <AppNavbar class="sticky top-0 z-50"/>

    <!-- Landing Content (fullscreen emphasis) -->
    <div class="flex flex-col justify-center min-h-screen relative">
      <CountDown class="pb-5"/>

      <div class="text-center space-y-4">
        <p class="text-4xl lg:text-6xl font-extralight">Join the first ever</p>
        <p class="text-4xl lg:text-6xl font-bold">Bebras Challenge</p>
        <p class="text-4xl lg:text-6xl font-extralight">in KISJ</p>
        <p class="text-lg lg:text-md font-light">Hosted by Easy Computing Club</p>
        <div class="py-30"></div>

      </div>

      <!-- Scroll Down Indicator -->
      <div class="absolute bottom-16 w-full text-center">
        <p class="text-white">Scroll Down</p>
        <svg class="w-6 h-10 mx-auto animate-bounce" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
             stroke="currentColor">
          <path d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
        </svg>
      </div>
    </div>

    <!-- Additional Content Below the Fold -->
    <div class="p-6 max-w-screen-lg mx-auto grid md:grid-cols-3 grid-cols-1 gap-4">
      <div>
        <p class="font-normal text-5xl">Introduction</p>
        <p class="font-light text-xl">The USA Bebras Challenge tests your logic and computational skills through
          different types
          of fun and challenging problems. Without touching a code</p>
      </div>

      <div v-if="domReady" :style="computeBoxStyle($el)" class="col-span-2">
        <img src="/src/assets/preview.png" alt="Bebras Challenge Problem Preview">
      </div>
    </div>

    <div class="p-6 max-w-screen-lg mx-auto grid md:grid-cols-2 grid-cols-1 gap-4">
      <div v-if="domReady" :style="computeBoxStyle($el)" class="glassmorphic-box space-y-4">
        <p class="text-2xl font-normal">Don't know coding?</p>
        <p class="font-light">No worries! Bebras Challenge requires no prior knowledge of computer science. All you need
          is logical thinking and problem-solving skills.</p>
        <p class="font-light">Sign up now! You don't know what you're missing out on!</p>
      </div>

      <div v-if="domReady" :style="computeBoxStyle($el)" class="glassmorphic-box space-y-4">
        <p class="text-2xl font-normal">Check out the official website!</p>
        <p class="font-light">Still not sure? Check out the <a href="https://challenge.bebraschallenge.org/"
                                                               target="_blank" rel="noopener noreferrer"
                                                               class="text-blue-400 hover:underline">Bebras Challenge official
          website</a> for more information!</p>
        <p class="font-light">They got rules, practice problems, last year's problems, and more! Definitely worth a
          visit!</p>
      </div>
    </div>

    <div class="grid grid-cols-1 align-s justify-items-center p-12">
      <div>
        Made with ❤️ by <a href="https://github.com/suhjae" target="_blank" rel="noopener noreferrer"
                           class="text-blue-400 hover:underline">SuhJae</a>
      </div>
    </div>

  </div>
</template>

<script setup>
import AppNavbar from "./components/AppNavbar.vue";
import {ref, onMounted, onBeforeUnmount, nextTick} from 'vue';
import CountDown from "./components/CountDown.vue";

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

