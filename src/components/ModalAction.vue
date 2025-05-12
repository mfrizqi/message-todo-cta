<script setup>
import TodoContainer from "./todo-list/container.vue"
import ChatContainer from "./chat/container.vue"
import Loading from "./utils/Loading.vue";

defineProps({
  isOpen: String,
});
</script>

<template>
  <Transition name="fade">
    <section v-if="isOpen">
      <div
        class="bg-white min-w-[500px] max-h-[75vh] max-w-[737px] min-h-[400px] rounded overflow-y-auto text-slate-500 mb-2"
      >
        <TodoContainer v-if="isOpen === 'task'"/>
        <ChatContainer v-if="isOpen === 'chat'"/>
      </div>
    </section>
  </Transition>
</template>

<style scoped>
.fade-enter-active {
  transition: all 0.3s ease-in-out;
}

.fade-leave-active {
  transition: all 0.2s ease-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
