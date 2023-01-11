<script setup>
import Countdown from "./components/Countdown.vue";
import data from "./json/data.json";
</script>

<template>
  <main class="main-app">
    <Countdown :time="data.event" :event_title="data.title" />
  </main>
</template>

<style scoped>
.main-app {
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(255, 255, 255);
}
</style>
