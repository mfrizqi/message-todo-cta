<script setup>
import { computed, ref, watch } from "vue";
const isFABOpen = ref(false);
const FABState = ref("");
</script>

<template lang="">
  <section class="relative w-full">
    <section
      class="flex flex-row-reverse gap-4 items-end"
    >
      <div
        class="rounded-full flex justify-center items-center p-[6px] bg-[#2F80ED] cursor-pointer"
        @click="isFABOpen = !isFABOpen"
      >
        <img src="../assets/img/icon/storm.svg" />
      </div>
      <Transition name="slide-fade">
        <div v-if="isFABOpen" class="flex gap-4">
          <div class="text-center cursor-pointer" @click="FABState = 'task'">
            <div class="mb-2 font-base">Task</div>
            <div
              class="rounded-full h-[60px] w-[60px] flex justify-center items-center p-[6px]"
              :class="{
                'bg-[#F2F2F2]': FABState !== 'task',
                'bg-[#F8B76B]': FABState === 'task',
              }"
            >
              <img src="../assets/img/icon/tasklist.svg" />
            </div>
          </div>
          <div class="text-center cursor-pointer" @click="FABState = 'chat'">
            <div class="mb-2 font-base">Inbox</div>
            <div
              class="rounded-full h-[60px] w-[60px] flex justify-center items-center p-[6px]"
              :class="{
                'bg-[#F2F2F2]': FABState !== 'chat',
                'bg-[#8785FF]': FABState === 'chat',
              }"
            >
              <img src="../assets/img/icon/chat.svg" />
            </div>
          </div>
        </div>
      </Transition>
    </section>
  </section>
</template>

<style scoped>
.slide-fade-enter-active {
  transition: all 0.3s ease-in-out;
}

.slide-fade-leave-active {
  transition: all 0.2s ease-out;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>
