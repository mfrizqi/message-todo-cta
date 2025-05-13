<script setup>
import { computed, ref, watch, defineEmits, nextTick, reactive } from "vue";

const emit = defineEmits(["open-modal"]);
let isFABOpen = ref(false);
let FABState = reactive({
  state: "",
});

const selectFAB = (value) => {
  FABState.state = value;
  emit("open-modal", value);
};

const setFABColor = computed(() => {
  let bgColor = "bg-[#2F80ED]";
  if (FABState.state === "task") {
    bgColor = "bg-[#F8B76B]";
  } else if (FABState.state === "chat") {
    bgColor = "bg-[#8785FF]";
  }
  return bgColor;
});

const toggleMainFAB = () => {
  if (FABState.state !== "") {
    FABState.state = "";
    emit("open-modal", false);
  }
  isFABOpen.value = !isFABOpen.value;
};

const toggleFAB = (name) => {
  if (name === FABState.state) {
    return false;
  }
  return true;
};
</script>

<template>
  <section class="relative w-full mt-2">
    <section class="flex flex-row-reverse gap-4" :class="{'items-end' : FABState.state === '', 'items-center' : FABState.state !== ''}">
      <div
        class="rounded-full flex justify-center items-center p-[6px] cursor-pointer h-[68px] w-[68px]"
        @click="toggleMainFAB()"
        :class="setFABColor"

      >
        <img v-if="FABState.state === ''" src="../assets/img/icon/storm.svg" />
        <img v-if="FABState.state === 'task'" src="../assets/img/icon/task_active.svg" class="w-[24px] h-[24px]"/>
        <img v-if="FABState.state === 'chat'" src="../assets/img/icon/chat_active.svg" class="w-[24px] h-[24px]"/>
      </div>
      <Transition name="slide-fade">
        <div v-if="isFABOpen" class="flex gap-4">
          <div v-if="toggleFAB('task')" class="text-center cursor-pointer" @click="selectFAB('task')">
              <div v-if="FABState.state === ''" class="mb-2 font-base">Task</div>
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
          <div v-if="toggleFAB('chat')" class="text-center cursor-pointer" @click="selectFAB('chat')">
              <div v-if="FABState.state === ''" class="mb-2 font-base">Inbox</div>
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
* {
  caret-color: transparent;
}

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
