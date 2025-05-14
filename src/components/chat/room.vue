<script setup>
import { defineEmits, onMounted, reactive, ref } from "vue";
import ChatBubble from "./ChatBubble.vue";
import { uuid } from "vue-uuid";
import axios from "axios";

defineProps({
  RoomMeta: {},
  color: String,
  bgColor: String,
});

const emit = defineEmits(["back-chat"]);
const message = ref("");
const loading = ref(false);
const loadingUser = ref(false);
const users = ref([]);

const room = ref({
  items: [
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      text: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Martin Joy",
      text: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Martin Joy",
      text: "Hello Obaidullah, I will be your case advisor for case #029290. I have assigned some homework for you to fill. Please keep up with the due dates. Should you have any questions, you can message me anytime. Thanks.",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "You",
      text: "Please contact Mary for questions regarding the case bcs she will be managing your forms from now on! Thanks Mary.",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "You",
      text: "No worries. It will be completed ASAP. I’ve asked him yesterday.",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      text: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "Obaidullah Amarkhil",
      text: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "You",
      text: "Morning. I’ll try to do them. Thanks",
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
      text: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
    {
      id: uuid.v4(),
      name: "You",
      text: "Morning. I’ll try to do them. Thanks",
      time: "19:32",
      type: "user",
    },
  ],
});

const backToChatList = () => {
  emit("back-chat");
};

const setupParticipants = async () => {
  loadingUser.value = true;
  const uniqueAttributes = {};

  console.log(room);

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
  let userNames = uniqueAttributes.name.filter(
    (name) => name.toLowerCase() !== "you"
  );

  await getUsers();

  if (users) {
    userNames.forEach((name) => {
      items = room.value.items.map((item) => {
        const chatItem = { ...item };
        if (chatItem.name !== "You") {
          if (chatItem.name === name) {
            chatItem.color = "green";
            chatItem.name = users.value[0].name;
          } else {
            chatItem.color = "orange";
            chatItem.name = users.value[1].name;
          }
        } else {
          chatItem.color = "purple";
        }
        return chatItem;
      });
    });
    room.value.items = [];
    room.value.items = JSON.parse(JSON.stringify(items));
    setTimeout(() => {
      loadingUser.value = false;
    }, 500);
  }
};

onMounted(() => {
  setupParticipants();
  const container = document.getElementById("chat-area");
  container.scrollTop = container.scrollHeight;
});

const getUsers = async () => {
  await axios
    .get("https://jsonplaceholder.typicode.com/users")
    .then((res) => {
      for (let i = 0; i < 2; i++) {
        let user = res.data[Math.floor(Math.random() * res.data.length)];
        users.value.push(user);
      }
    })
    .catch((err) => {
      console.error(err.message);
    })
    .finally(() => {
      console.log(users);
    });
};

const sendChat = async () => {
  if (message.value === "") return;

  const payload = {
    id: uuid.v4(),
    name: "You",
    text: message.value,
    time: "19:32",
    type: "user",
    color: "purple",
  };

  loading.value = true;
  await axios
    .post("https://jsonplaceholder.typicode.com/posts", payload, {
      headers: {
        "Content-type": "application/json; charset=UTF-8",
      },
    })
    .then((res) => {
      console.log(res);
      message.value = "";
    })
    .catch((err) => {
      console.error(err.message);
    })
    .finally(() => {
      loading.value = false;
    });

  room.value.items.push(payload);

  setTimeout(() => {
    const container = document.getElementById("chat-area");
    container.scrollTop = container.scrollHeight;
  }, 10);
};

const deleteHandler = (id) => {
  room.value.items = room.value.items.filter((chat) => chat.id !== id);
};
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
        <div class="text-xs" v-if="RoomMeta.participants > 0">
          {{ RoomMeta.participants }} participants
        </div>
      </div>
      <img
        src="../../assets/img/icon/x.svg"
        class="h-[18px] w-[18px] cursor-pointer"
      />
    </div>
    <section
      v-if="!loadingUser"
      class="px-5 overflow-y-auto py-4"
      id="chat-area"
    >
      <template v-for="chat in room.items" :key="chat.id">
        <div v-if="chat.type === 'date'" class="flex w-full flex-col">
          <div className="divider divider-neutral">Today, June 09, 2021</div>
        </div>
        <ChatBubble
          v-if="chat.type === 'user'"
          :chat="chat"
          @delete-chat="deleteHandler"
        />
      </template>
    </section>
    <div v-if="loadingUser" class="flex w-full h-full flex-col gap-4 py-4 px-5">
      <div class="skeleton bg-gray-300 h-28 w-72"></div>
      <div class="skeleton bg-gray-300 h-28 w-72 self-end"></div>
      <div class="skeleton bg-gray-300 h-28 w-72"></div>
    </div>
    <div class="flex pb-4 px-5 gap-2">
      <input
        type="text"
        class="grow border border-gray-500 rounded px-2 outline-none"
        placeholder="Type a new message"
        v-model="message"
        :class="{ 'opacity-50': loading }"
        :disabled="loading"
      />
      <button
        class="bg-[#2F80ED] px-4 py-1 rounded text-white cursor-pointer"
        @click="sendChat()"
        @keyup.enter="sendChat()"
        :disabled="loading"
        :class="{ 'opacity-70': loading }"
      >
        Send
        <span
          v-if="loading"
          class="loading loading-spinner loading-xs ml-1"
        ></span>
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
  }
}

.skeleton {
  border-radius: var(--radius-box);
  /* background-color: var(--color-base-300); */
  @media (prefers-reduced-motion: reduce) {
    transition-duration: 15s;
  }
  will-change: background-position;
  animation: skeleton 1.8s ease-in-out infinite;
  background-image: linear-gradient(
    105deg,
    #e4141400 0% 40%,
    #ffffff97 50%,
    #87878700 60% 100%
  );
  background-size: 200% auto;
  background-repeat: no-repeat;
  background-position-x: -50%;
}
</style>