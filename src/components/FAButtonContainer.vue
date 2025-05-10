<script setup>
import { computed, ref, watch, defineEmits, nextTick, reactive } from "vue";


const emit = defineEmits(['open-modal']);
const isFABOpen = ref(false);
let FABState = reactive({
  state: ''
});

const selectFAB = (value) => {
  FABState.state = value;
  emit('open-modal', value)
  // console.log(FABState)
  nextTick()
  
};
</script>

<template lang="">
  <section class="relative w-full">
    <section class="flex flex-row-reverse gap-4 items-end">
      <div
        class="rounded-full flex justify-center items-center p-[6px] bg-[#2F80ED] cursor-pointer"
        @click="isFABOpen = !isFABOpen"
      >
        <img src="../assets/img/icon/storm.svg" />
      </div>
      <Transition name="slide-fade">
        <div v-if="isFABOpen" class="flex gap-4">
          <div class="text-center cursor-pointer" @click="selectFAB('task')">
            <Transition name="title-fade">
              <div v-if="FABState.state === ''" class="mb-2 font-base">Task</div>
            </Transition>
            <div
              class="rounded-full h-[60px] w-[60px] flex justify-center items-center p-[6px]"
              :class="{
                'bg-[#F2F2F2]': FABState.state !== 'task',
                'bg-[#F8B76B]': FABState.state === 'task',
              }"
            >
              <img src="../assets/img/icon/tasklist.svg" />
            </div>
          </div>
          <div class="text-center cursor-pointer" @click="selectFAB('chat')">
            <Transition name="title-fade">
              <div v-if="FABState.state === ''" class="mb-2 font-base">Inbox</div>
            </Transition>
            <div
              class="rounded-full h-[60px] w-[60px] flex justify-center items-center p-[6px]"
              :class="{
                'bg-[#F2F2F2]': FABState.state !== 'chat',
                'bg-[#8785FF]': FABState.state === 'chat',
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

.title-fade-enter-active {
  transition: all 0.3s ease-in-out;
}

.title-fade-leave-active {
  transition: all 0.2s ease-out;
}

.title-fade-enter-from,
.title-fade-leave-to {
  opacity: 0;
}
</style>
