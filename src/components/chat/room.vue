<script setup>
import { defineEmits, onMounted, reactive, ref } from "vue";
import ChatBubble from "./ChatBubble.vue";
import { uuid } from "vue-uuid";

defineProps({
  RoomMeta: {},
  color: String,
  bgColor: String,
});

const emit = defineEmits(["back-chat"]);

const room = ref({
  items: [
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      chat: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Martin Joy",
      chat: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Martin Joy",
      chat: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      chat: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      chat: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      date: "June 09, 2021",
      type: "date",
    },
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      chat: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      chat: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
  ],
});

const backToChatList = () => {
  emit("back-chat");
};

const setupColor = () => {
  const uniqueAttributes = {};

  console.log(room)

  room.value.items.forEach((obj) => {
    for (const key in obj) {
      if (obj.hasOwnProperty(key)) {
        if (!uniqueAttributes[key]) {
          uniqueAttributes[key] = [];
        }
        if (!uniqueAttributes[key].includes(obj[key])) {
          uniqueAttributes[key].push(obj[key]);
        }
      }
    }
  });
  console.log(uniqueAttributes);
  let items = [];
  uniqueAttributes.name.forEach((name) => {
    items = room.value.items.map((item) => {
      const chatItem = { ...item };
      if (chatItem.name === name) {
        chatItem.color = 'green'
      } else {
        chatItem.color = 'orange'
      }
      return chatItem;
    });
  });
  room.value.items = []
  room.value.items = JSON.parse(JSON.stringify(items));
  console.log(room.items)
};

onMounted(() => {
  setupColor();
});
</script>

<template>
  <section class="flex flex-col justify-between h-full">
    <div class="flex w-full gap-4 border-b border-gray-500 px-8 py-5">
      <img
        src="../../assets/img/icon/arrow-left.svg"
        class="h-[24px] w-[24px] cursor-pointer"
        @click="backToChatList()"
      />
      <div class="grow">
        <div class="text-[#2F80ED] text-md">{{ RoomMeta.title }}</div>
        <div class="text-xs">3 participants</div>
      </div>
      <img
        src="../../assets/img/icon/x.svg"
        class="h-[18px] w-[18px] cursor-pointer"
      />
    </div>
    <div class="px-5 overflow-y-auto py-4">
      <template v-for="chat in room.items" :key="chat.id">
        <div v-if="chat.type === 'date'" class="flex w-full flex-col">
          <div className="divider divider-neutral">Today, June 09, 2021</div>
        </div>
        <ChatBubble
          :chat="chat"
        />
      </template>
    </div>
    <div class="flex pb-4 px-5 gap-2">
      <input
        type="text"
        class="grow border border-gray-500 rounded px-2 outline-none"
        placeholder="Type a new message"
      />
      <button class="bg-[#2F80ED] px-4 py-1 rounded text-white cursor-pointer">
        Send
      </button>
    </div>
  </section>
</template>
<script setup>
</script>
<style scoped>
.divider {
  &:before,
  &:after {
    content: "";
    height: 1px;
    width: 100%;
    flex-grow: 1;
    /* background-color: var(--divider-color); */
  }
}
</style>