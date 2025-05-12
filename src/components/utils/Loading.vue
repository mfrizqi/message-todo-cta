<script setup>
defineProps({
  title: String,
});
</script>

<template>
  <div class="flex">
    <span className="loading loading-spinner loading-md"></span>
    {{ title }}
  </div>
</template>

<style>
</style>