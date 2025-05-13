<script setup>
defineProps({
    chat: {}
})

const getColor = (chat)=>{
    return `text-[#${chat.color}]`
}
const getBgColor = (chat)=>{
    return `bg-[#${chat.bgColor}]`
}

</script>

<template>
  <div class="mb-2.5 last:mb-0">
    <div class="mb-2" :class="getColor(chat)">{{ chat.name }}</div>
    <div class="flex items-start gap-2">
      <div class="rounded w-[fit-content] p-2.5 text-[#4F4F4F]" :class="getBgColor(chat)">
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
</style>