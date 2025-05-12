<script setup>
import Loading from "../utils/Loading.vue";
import ChatCard from "./card.vue"
</script>

<template>
  <section>
    <div class="flex">
      <!-- <Loading title="Loading Chats..."></Loading> -->
      <div class="input w-full px-8 mx-6 mt-5 bg-white border border-gray-400 text-gray-800 h-[32px]">
        <input type="search" class="grow" placeholder="Search" />
        <svg
          class="h-[1em] opacity-50"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
        >
          <g
            stroke-linejoin="round"
            stroke-linecap="round"
            stroke-width="2.5"
            fill="none"
            stroke="#1e2939"
          >
            <circle cx="11" cy="11" r="8"></circle>
            <path d="m21 21-4.3-4.3"></path>
          </g>
        </svg>
      </div>
    </div>
    <section class="px-8 pt-5.5">
      <ChatCard/>
    </section>
  </section>
</template>

<style scoped>

</style>
