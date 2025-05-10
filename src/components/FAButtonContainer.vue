<template lang="">
  <section
    class="absolute right-[24px] bottom-[24px] flex flex-row-reverse gap-4 items-end"
  >
    <div
      class="rounded-full flex justify-center items-center p-[6px] bg-[#2F80ED] cursor-pointer"
      @click="
        () => {
          isFABOpen = !isFABOpen;
        }
      "
    >
      <img src="../assets/img/icon/storm.svg" alt="" />
    </div>
    <div v-if="isFABOpen" class="text-center cursor-pointer">
      <div class="mb-2 font-medium">Inbox</div>
      <div
        class="rounded-full bg-[#F2F2F2] h-[60px] w-[60px] flex justify-center items-center p-[6px]"
      >
        <img src="../assets/img/icon/chat.svg" alt="" />
      </div>
    </div>
    <div  v-if="isFABOpen" class="text-center cursor-pointer">
      <div class="mb-2 font-medium">Task</div>
      <div
        class="rounded-full bg-[#F2F2F2] h-[60px] w-[60px] flex justify-center items-center p-[6px]"
      >
        <img src="../assets/img/icon/tasklist.svg" alt="" />
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

defineProps({
  msg: String,
});

const isFABOpen = ref(false);
</script>

<style lang=""></style>
