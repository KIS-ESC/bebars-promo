<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';

const eventDate = new Date("2023-11-14T15:45:00+09:00");
const day = ref(0);
const hour = ref(0);
const minute = ref(0);
const second = ref(0);

const calculateRemainingTime = () => {
  const now = new Date();
  const diff = eventDate - now;

  if (diff <= 0) {
    day.value = 0;
    hour.value = 0;
    minute.value = 0;
    second.value = 0;
    return;
  }

  day.value = Math.floor(diff / (1000 * 60 * 60 * 24));
  hour.value = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  minute.value = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
  second.value = Math.floor((diff % (1000 * 60)) / 1000);
};

let interval;

onMounted(() => {
  calculateRemainingTime();
  interval = setInterval(calculateRemainingTime, 1000);
});

onBeforeUnmount(() => {
  clearInterval(interval);
});
</script>

<template>
  <div class="grid grid-cols-1 align-s justify-items-center">
    <div class="grid grid-cols-4 gap-4 max-w-md align-s justify-items-center font-light text-xl">
      <div>
        {{ day }} d
      </div>

      <div>
        {{ hour }} h
      </div>

      <div>
        {{ minute }} m
      </div>

      <div>
        {{ second }} s
      </div>
    </div>

    <div class="p-3 font-extralight text-md">Nov 14th, 15:45-16:45 @ HS Library</div>
  </div>
</template>
