<script setup>
import FloatingActionButton from "./components/FAButtonContainer.vue";
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <div class="relative h-svh">
    <FloatingActionButton msg="Hello msg" />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
