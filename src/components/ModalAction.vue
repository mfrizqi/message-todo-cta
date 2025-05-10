<script setup>
import TodoCard from "./todo-list/card.vue";

defineProps({
  isOpen: Boolean,
})

</script>

<template lang="">
  <section v-if="isOpen">
    <div
      class="bg-white min-w-[500px] max-h-[600px] min-h-[400px] rounded scroll-auto overflow-y-auto text-slate-500"
    >
      <div
        class="sticky top-0 bg-white h-full pt-4.5 pb-5 flex justify-between px-2"
      >
        <div className="dropdown">
          <div tabIndex="{0}" role="button" className="btn m-1">My tasks</div>
          <ul
            tabIndex="{0}"
            className="dropdown-content menu bg-base-100 rounded-box z-1 w-52 p-2 shadow-sm"
          >
            <li><a>Personal Errands</a></li>
            <li><a>Urgent To-Do</a></li>
          </ul>
        </div>
        <button className="btn btn-primary">New Task</button>
      </div>
      <div class="h-[900px] pl-7">
        <TodoCard></TodoCard>
      </div>
    </div>
  </section>
</template>

<style lang=""></style>
