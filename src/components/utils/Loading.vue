<script setup>
defineProps({
  title: String,
});
</script>

<template>
  <div class="flex flex-col items-center">
    <span className="loading loading-spinner loading-md"></span>
    {{ title }}
  </div>
</template>

<style>
</style>