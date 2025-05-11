<script setup>
import { ref } from "vue";
import FAB from "./components/FAButtonContainer.vue";
import ModalAction from "./components/ModalAction.vue";

const openModal = () => {};
let isOpen = ref(false)


const modalHandler = (value)=>{
  console.log(value)
  if(value){
    isOpen.value = true
  } else {
    isOpen.value = false
  }
}

</script>

<template>
  <div class="relative h-svh">
    <section
      class="h-svh w-full flex flex-col justify-end items-end absolute right-[24px] bottom-[24px]"
    >
      <ModalAction :isOpen="isOpen" />
      <FAB @open-modal="modalHandler" />
    </section>
  </div>
</template>

<style scoped>
* {
  caret-color: transparent;
}

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
