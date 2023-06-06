<template>
  <div>
    <div>Welcome, Mike</div>
    <div>It is {{ currentTime }}</div>
    <button @click="changeTimeZone('UTC')">UTC</button>
    <button @click="changeTimeZone('America/New_York')">EST</button>
    <button @click="changeTimeZone('Asia/Kolkata')">India</button>
    <button @click="changeTimeZone('America/Chicago')">Texas</button>
    <button @click="changeTimeZone('America/Los_Angeles')">California</button>
    <button @click="changeTimeZone('Europe/London')">UK</button>
    <button @click="changeTimeZone('Europe/Amsterdam')">Amsterdam</button>
  </div>
</template>
<script setup lang="ts">
import { onBeforeUnmount, ref } from "vue";

const currentTimeZone = ref("UTC");
const currentTime = ref("");
const animationFrameId = ref(0);

const updateTime = () => {
  currentTime.value = new Date().toLocaleString(undefined, {
    timeZone: currentTimeZone.value,
  });
  animationFrameId.value = requestAnimationFrame(updateTime);
};

const changeTimeZone = (timeZone: string) => {
  currentTimeZone.value = timeZone;
};

updateTime();

onBeforeUnmount(() => {
  cancelAnimationFrame(animationFrameId.value);
});
</script>
