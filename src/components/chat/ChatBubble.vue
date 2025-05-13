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

const isSender = (name)=>{
  return  name.toLowerCase() === 'you'
}

onMounted(() => {
  console.log(props);
});
</script>

<template>
  <div class="mb-2.5 last:mb-0 flex flex-col">
    <div class="mb-2" :class="[setTextColor(chat), {'text-right': isSender(chat.name)}]">
      {{ chat.name }}
    </div>
    <div class="flex items-start gap-2" :class="{'flex-row-reverse' : isSender(chat.name)}">
      <div class="rounded w-[fit-content] max-w-md p-2.5 text-[#4F4F4F]" :class="setBgColor(chat)">
        {{ chat.text }}
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

.purple-text {
  color: #9B51E0;
}
.purple-bg {
  background-color: #EEDCFF;
}

</style>