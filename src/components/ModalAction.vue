<script setup>
import TodoCard from "./todo-list/card.vue";

defineProps({
  isOpen: String,
});
</script>

<template>
  <Transition name="fade">
    <section v-if="isOpen">
      <div
        class="bg-white min-w-[500px] max-h-[747px] max-w-[737px] min-h-[400px] rounded overflow-y-auto text-slate-500 mb-2"
      >
        <section v-if="isOpen === 'task'">
          <div
            class="sticky top-0 bg-white h-full pt-4.5 pb-5 flex items-center justify-between px-2 z-10"
          >
            <div className="dropdown">
              <div
                tabIndex="{0}"
                role="button"
                className="btn m-1 bg-white shadow-none border border-gray-500 text-gray-600 font-semibold px-3.5 py-2.5 flex justify-between"
              >
                My tasks
                <img
                  src="../assets/img/icon/chevron-down.svg"
                  class="h-[20px] w-[20px]"
                />
              </div>
              <ul
                tabIndex="{0}"
                className="dropdown-content menu rounded-box z-1 w-52 p-0 shadow-sm bg-white border border-gray-500 text-gray-600 "
              >
                <li class="border-b border-gray-500 font-semibold p-0">
                  <a>Personal Errands</a>
                </li>
                <li class="font-semibold p-0"><a>Urgent To-Do</a></li>
              </ul>
            </div>
            <button
              className="btn bg-[#2F80ED] border-0 shadow-none px-4 py-3.5"
            >
              New Task
            </button>
          </div>
          <div class="min-h-[400px] pl-7 pr-2.5">
            <TodoCard></TodoCard>
          </div>
        </section>
        <section v-if="isOpen == 'chat'">
          Chat Section
        </section>
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
