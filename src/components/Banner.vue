<script setup>
defineProps({ title: String });
</script>

<template>
  <h1 class="title">{{ title }}</h1>
</template>

<style>
.copyright {
  position: fixed;
  bottom: 1rem;
  right: 1rem;
}
</style>
