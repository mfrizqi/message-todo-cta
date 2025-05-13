<script setup>
import { onMounted } from "vue";

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

onMounted(() => {
  console.log(props);
});
</script>

<template>
  <div class="mb-2.5 last:mb-0">
    <div class="mb-2" :class="setTextColor(chat)">
      {{ chat.name }}
    </div>
    <div class="flex items-start gap-2">
      <div class="rounded w-[fit-content] p-2.5 text-[#4F4F4F]" :class="setBgColor(chat)">
        Morning. I’ll try to do them. Thanks
        <div>19:32</div>
      </div>
      <img
        src="../../assets//img/icon/more-horizontal.svg"
        class="w-[16px] h-[16px] cursor-pointer"
        alt=""
      />
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
</style>