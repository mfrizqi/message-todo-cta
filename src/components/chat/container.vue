<script setup>
import { onMounted, reactive, ref } from "vue";

import Loading from "../utils/Loading.vue";
import ChatListCard from "./card.vue";
import Chatroom from "./room.vue";
import { uuid } from "vue-uuid";

const chat = reactive({
  room: [
    {
      id: uuid.v4(),
      title: "109220-Naturalization",
      date: "January 1,2021 19:10",
      name: "Cameron Phillips",
      description: "Please check this out!",
      isNew: true,
      isConvo: true,
      participants: 3,
    },
    {
      id: uuid.v4(),
      title:
        "Jeannette Moraima Guaman Chamba (Hutto I-589) [ Hutto Follow Up - Brief Service ]",
      date: "02/06/2021 10:45",
      name: "Ellen",
      description: "Hey, please read.",
      isNew: false,
      isConvo: true,
      participants: 3,
    },
    {
      id: uuid.v4(),
      title: "8405-Diana SALAZAR MUNGUIA",
      date: "01/06/2021 12:19",
      name: "Cameron Phillips",
      description:
        "I understand your initial concerns and thats very valid, Elizabeth. But you need to look over from the company perspective",
      isNew: false,
      isConvo: true,
      participants: 2,
    },
    {
      id: uuid.v4(),
      title: "FastVisa Support",
      date: "01/06/2021 12:19",
      name: "FastVisa",
      description: "Hey there! Welcome to your inbox.",
      isNew: false,
      isConvo: false,
      participants: 0,
    },
  ],
  state: "list",
  data: {},
});

const loadingSearch = ref(true);
const searchKey = ref("");

const chatRoomOrigin = JSON.parse(JSON.stringify(chat.room));

const selectChatroom = (room) => {
  chat.state = room.id;
  chat.data = room;
};

const backChatHandler = () => {
  chat.state = "list";
};

const handleSearch = (value) => {
  loadingSearch.value = true;
  setTimeout(() => {
    if (value !== "") {
      searchKey.value = value;
      chat.room = chatRoomOrigin.filter((room) => room.title.toLowerCase().includes(value));
    } else {
      chat.room = chatRoomOrigin;
      searchKey.value = "";
    }

    loadingSearch.value = false;
  }, 300);
};

onMounted(() => {
  setTimeout(() => {
    loadingSearch.value = false;
  }, 500);
});
</script>

<template>
  <section class="h-full">
    <section
      class="h-full"
      v-if="chat.state === 'list'"
      :class="{ 'overflow-hidden': loadingSearch }"
    >
      <div class="flex sticky top-0 bg-white z-20 pb-5.5">
        <div
          class="input w-full px-8 mx-6 mt-6 bg-white border border-gray-400 text-gray-800 h-[32px]"
        >
          <input
            type="search"
            class="grow"
            placeholder="Search"
            @keyup="handleSearch($event.target.value)"
          />
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
      <div
        v-if="loadingSearch"
        class="loading-container flex flex-col items-center justify-center"
      >
        <Loading title="Loading Chats ..."></Loading>
      </div>
      <div class="px-8" v-if="!loadingSearch && chat.room.length > 0">
        <ChatListCard
          v-for="room in chat.room"
          :key="room.id"
          :room="room"
          @click="selectChatroom(room)"
        />
      </div>
      <div
        class="not-found-container flex flex-col items-center justify-center"
        v-if="chat.room.length === 0"
      >
        <span><strong class="text-gray-700">{{ searchKey }}</strong> is not found</span>
      </div>
    </section>
    <section v-if="chat.state !== 'list'" class="h-full">
      <Chatroom @back-chat="backChatHandler()" :RoomMeta="chat.data" />
    </section>
  </section>
</template>

<style scoped>
.loading-container,
.not-found-container {
  height: calc(100% - 108px);
}
</style>
