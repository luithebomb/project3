<script setup>
import { ref } from 'vue';

const timeInput = ref(0);
const countdownDisplay = ref(0);
let countdownInterval = null;

const startCountdown = () => {
  let time = parseInt(timeInput.value);

  if (isNaN(time) || time < 1 || time > 60) {
    alert("Please enter a valid number between 1 and 60.");
    return;
  }

  countdownDisplay.value = time;
  clearInterval(countdownInterval);

  countdownInterval = setInterval(() => {
    time--;
    countdownDisplay.value = time;

    if (time <= 0) {
      clearInterval(countdownInterval);
      alert("Time is up!");
    }
  }, 1000);
};
</script>

<template>
  <div>
    <h1 class="main-title">Countdown Timer</h1>
    <h2>by Luis Pena</h2>

    <div class="input-container">
      <label for="timeInput">Enter time (in seconds, max 60):</label>
      <input type="number" id="timeInput" v-model="timeInput" min="1" max="60" placeholder="Enter seconds">
      <button @click="startCountdown">Start Timer</button>
    </div>

    <div class="countdown-container">
      <div class="circle">
        <span>{{ countdownDisplay }}</span>
      </div>
    </div>
  </div>
</template>

