<script setup>
defineProps({
  room: {},
});

const getInitialName = (name)=>{
  return name[0]
}

</script>

<template>
  <section
    class="flex gap-4 text-sm border-b border-gray-500 pb-5.5 pt-6 relative cursor-pointer first:pt-0 last:border-0"
  >
    <div class="relative" v-if="room.isConvo">
      <div
        class="h-[34px] w-[34px] rounded-full bg-[#2F80ED] relative left-[6px] z-10 flex justify-center items-center"
      >
        <img src="../../assets//img//icon/user.svg" class="w-[20px] h-[20px]" />
      </div>
      <div
        class="h-[34px] w-[34px] rounded-full bg-[#E0E0E0] absolute top-0 left-[-10px] flex justify-center items-center"
      >
        <img
          src="../../assets//img//icon/person_grey.svg"
          class="w-[20px] h-[20px] grayscale"
        />
      </div>
    </div>
    <div v-if="!room.isConvo">
      <div
        class="h-[34px] w-[34px] rounded-full bg-[#2F80ED] relative z-10 flex justify-center items-center"
      >
        <div class="text-white">{{ getInitialName(room.name) }}</div>
      </div>
    </div>
    <div>
      <div class="flex gap-4">
        <div class="font-bold text-[#2F80ED]">{{ room.title }}</div>
        <div class="grow shrink-0">{{ room.date }}</div>
      </div>
      <section>
        <div class="font-bold text-sm">{{ room.name }} :</div>
        <div class="line-clamp-1">{{ room.description }}</div>
      </section>
    </div>
    <div v-if="room.isNew" class="absolute bg-[#EB5757] h-[10px] w-[10px] rounded-full right-0 bottom-[22px]"></div>
  </section>
</template>

<style lang=""></style>
