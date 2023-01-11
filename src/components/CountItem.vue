<script setup>
import { computed, defineProps, watch } from "vue";
const props = defineProps({
  value: Number,
});
const parseValue = computed(() => {
  return String(props.value).padStart(2, "0");
});
</script>
<template>
  <div class="count-item">
    {{ parseValue }}
  </div>
</template>

<style>
.count-item {
  font-size: min(10vw, 8rem);
  user-select: none;
  aspect-ratio: 1 / 1;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: #e0e0e0;
  border-radius: 20px;
  box-shadow: 14px 14px 24px #bcbcbc, -14px -14px 24px #ffffff;
}
</style>
