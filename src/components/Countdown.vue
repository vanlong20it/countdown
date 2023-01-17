<script setup>
import { reactive, defineProps, ref, onMounted } from "vue";
import CountItem from "./CountItem.vue";
import Banner from "./Banner.vue";
const props = defineProps({
  time: String,
  event_title: String,
});
const hasExpired = ref(false);
const timer = reactive({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

const SECONDS_PER_DAY = 24 * 60 * 60;
const SECONDS_PER_HOUR = 60 * 60;
const SECONDS_PER_MINUTE = 60;

/**
 * 10000s
 * 100s
 *
 */

onMounted(() => {
  if (timeToParse() < 0) {
    hasExpired.value = true;
  }
  const interval = setInterval(() => {
    if (timeToParse() < 0) {
      clearInterval(interval);
    }
    timer.days = remainDays();
    timer.hours = remainHours();
    timer.minutes = remainMinutes();
    timer.seconds = remainSeconds();
  }, 1000);
});

const remainDays = () => {
  return Math.floor(timeToParse() / SECONDS_PER_DAY);
};

const remainHours = () => {
  return Math.floor(
    (timeToParse() % SECONDS_PER_DAY) / SECONDS_PER_HOUR
  );
};

const remainMinutes = () => {
  return Math.floor(
    (timeToParse() % SECONDS_PER_HOUR) / SECONDS_PER_MINUTE
  );
};

const remainSeconds = () => {
  return Math.floor(
    timeToParse() % SECONDS_PER_MINUTE
  );
};

const timeToParse = () => {
  return Math.floor(
    (new Date(props.time).getTime() - new Date().getTime()) / 1000
  );
};
</script>
<template>
  <div class="countdown">
    <Banner :title="props.event_title" />
    <h2 v-if="hasExpired" class="alert-title">Event has expired!</h2>
    <div class="countdown-list" v-if="!hasExpired">
      <li>
        <CountItem :value="timer.days" />
      </li>
      <li>
        <CountItem :value="timer.hours" />
      </li>
      <li>
        <CountItem :value="timer.minutes" />
      </li>
      <li>
        <CountItem :value="timer.seconds" />
      </li>
    </div>
  </div>
</template>
<style lang="scss">
.countdown {
  width: 100%;
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
  .title {
    font-size: 2rem;
    color: red;
    text-align: center;
    text-transform: uppercase;
    margin-bottom: 2rem;
    @media (min-width: 768px) {
      font-size: 4rem;
    }
  }
  &-list {
    list-style: none;
    justify-content: center;
    align-items: center;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 30px;
  }
  .alert-title {
    text-align: center;
  }
}
</style>
