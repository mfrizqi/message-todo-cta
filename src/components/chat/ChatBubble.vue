<script setup>
import { onMounted, defineEmits } from "vue";

const emit = defineEmits(["delete-chat"]);

const props = defineProps({
  chat: {},
  colorClass: String,
  bgColorClass: String,
});

const setTextColor = (chat) => {
  if (chat.color === "green") return "green-text";
  if (chat.color === "orange") return "orange-text";
  if (chat.color === "purple") return "purple-text";
};
const setBgColor = (chat) => {
  if (chat.color === "green") return "green-bg";
  if (chat.color === "orange") return "orange-bg";
  if (chat.color === "purple") return "purple-bg";
};

const isSender = (name) => {
  return name.toLowerCase() === "you";
};

const deleteChat = (id)=>{
  emit('delete-chat', id)
}

onMounted(() => {
});
</script>

<template>
  <div class="mb-2.5 last:mb-0 flex flex-col">
    <div
      class="mb-2"
      :class="[setTextColor(chat), { 'text-right': isSender(chat.name) }]"
    >
      {{ chat.name }}
    </div>
    <div
      class="flex items-start gap-2"
      :class="{ 'flex-row-reverse': isSender(chat.name) }"
    >
      <div
        class="rounded w-[fit-content] max-w-md p-2.5 text-[#4F4F4F]"
        :class="setBgColor(chat)"
      >
        {{ chat.text }}
        <div>19:32</div>
      </div>
      <div class="dropdown">
        <div tabindex="0" role="button" class="cursor-pointer">
          <img
            src="../../assets/img/icon/more-horizontal.svg"
            class="h-[16px] w-[16px] shrink-0"
          />
        </div>
        <div
          tabindex="0"
          class="dropdown-content card card-sm bg-white z-1 border border-gray-600 outline-none w-30 p-1"
        >
          <div class="card-body p-0 border-gray-600">
            <div
              class="active:bg-gray-100 text-[#EB5757] cursor-pointer px-3 py-2 transition-all border-gray-600"
              @click="deleteChat(chat.id)"
            >
              Delete
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.green-text {
  color: #43b78d;
}
.green-bg {
  background-color: #d2f2ea;
}

.orange-text {
  color: #e5a443;
}
.orange-bg {
  background-color: #fceed3;
}

.purple-text {
  color: #9b51e0;
}
.purple-bg {
  background-color: #eedcff;
}
</style>