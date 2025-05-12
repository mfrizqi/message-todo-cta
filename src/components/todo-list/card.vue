<script setup>
import "cally";
import { defineEmits } from "vue";

defineProps({
  todo: {},
});

const emit = defineEmits(["delete-todo"]);

const formatDate = (rawDate) => {
  const split_date = rawDate.split("-");
  const join_date = split_date[2] + "/" + split_date[1] + "/" + split_date[0];
  return join_date;
};

const handleChangeDate = (event, todo) => {
  const formated = formatDate(event.target.value);
  document.getElementById(`cally-${todo.id}`).innerText = formated;
  todo.date = formated;
};

const handleOpen = (todo) => {
  if (todo.isOpen) {
    todo.isEdit = false;
  }
  todo.isOpen = !todo.isOpen;
};

const handleChangeTitle = (todo, event) => {
  todo.title = event.target.value;
};

const toggleEdit = (todo) => {
  if (!todo.isOpen) return;
  todo.isEdit = !todo.isEdit;
};

const deleteTodo = (id) => {
  emit("delete-todo", id);
};

const calculateDays = (todo) => {
  if (todo.date === "") return;
  const rawCreated = todo.createdAt.split("/");
  const formatCreated =
    rawCreated[1] + "/" + rawCreated[0] + "/" + rawCreated[2];
  const rawDate = todo.date.split("/");
  const formatDate = rawDate[1] + "/" + rawDate[0] + "/" + rawDate[2];

  const dateCreated = new Date(formatCreated);
  const dateTask = new Date(formatDate);
  const diffTime = dateTask - dateCreated;
  const diffDays = Math.floor(diffTime / (1000 * 60 * 60 * 24));
  if (diffDays < 0) {
    return "Overdue";
  } else {
    return diffDays;
  }
};
</script>
<template>
  <section class="w-full flex gap-4 border-b border-gray-900 text-sm pb-5 mb-5">
    <div>
      <input
        type="checkbox"
        defaultChecked
        :checked="todo.checked"
        @change="todo.checked = !todo.checked"
        class="checkbox text-gray-500 rounded-sm h-[20px] w-[20px] border-2 border-gray-500 checked:shadow-none mt-1"
      />
    </div>
    <div class="flex flex-col gap-6 grow">
      <div class="flex justify-between">
        <div
          v-if="!todo.isEdit"
          class="font-semibold text-wrap shrink w-xs"
          :class="{
            'line-through text-gray-500': todo.checked,
            'text-gray-700': !todo.checked,
          }"
          @click="toggleEdit(todo)"
        >
          {{ todo.title !== "" ? todo.title : "Untitled" }}
        </div>
        <input
          v-if="todo.isEdit"
          type="text"
          @change="handleChangeTitle(todo, $event)"
          v-model="todo.title"
          class="border border-gray-500 px-4 py-2 rounded outline-none w-3xs pointer-events-auto text-gray-700 mr-4"
          placeholder="Type Task Title"
        />
        <div class="flex gap-2">
          <div
            class="shrink-0"
            :class="{
              invisible:
                todo.checked || todo.createdAt === '' || todo.date === '',
              'text-[#4F4F4F]': calculateDays(todo) > 10,
              'text-[#EB5757]': calculateDays(todo) < 10 || calculateDays(todo) === 'Overdue',
            }"
          >
            {{ calculateDays(todo) }}
            <span v-if="calculateDays(todo) >= 0">
              day<span v-if="calculateDays(todo) > 1">s</span> left
            </span>
          </div>
          <div class="text-gray-700 shrink-0">{{ todo.createdAt }}</div>
          <img
            v-if="todo.isOpen"
            @click="handleOpen(todo)"
            src="../../assets/img/icon/chevron-up.svg"
            class="h-[16px] w-[16px] shrink-0 cursor-pointer"
          />
          <img
            v-if="!todo.isOpen"
            @click="handleOpen(todo)"
            src="../../assets/img/icon/chevron-down.svg"
            class="h-[16px] w-[16px] shrink-0 cursor-pointer"
          />
          <div>
            <!-- Delete Todo Button -->
            <button
              class="bg-white shadow-none border-none p-0 cursor-pointer"
              :popovertarget="`popover-${todo.id}`"
              :style="{ 'anchor-name': `--anchor-${todo.id}` }"
            >
              <img
                src="../../assets/img/icon/more-horizontal.svg"
                class="h-[16px] w-[16px] shrink-0"
              />
            </button>
            <ul
              class="dropdown dropdown-end menu rounded-box bg-white border border-gray-600 w-30 p-0"
              popover
              :id="`popover-${todo.id}`"
              :style="{ 'position-anchor': `--anchor-${todo.id}` }"
            >
              <li class="text-[#EB5757]">
                <a
                  class="active:bg-white focus:bg-white enabled:bg-white px-3 py-2"
                  @click="deleteTodo(todo.id)"
                  >Delete</a
                >
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div v-if="todo.isOpen" class="flex gap-3 text-gray-700 items-center">
        <img
          src="../../assets/img/icon/clock.svg"
          class="h-[20px] w-[20px]"
          :class="{ grayscale: todo.date === '' }"
        />
        <div>
          <button
            :popovertarget="`cally-popover-${todo.id}`"
            class="input input-border bg-white border border-gray-500 rounded w-[194px] flex justify-between"
            :style="{ 'anchor-name': `--cally-${todo.id}` }"
          >
            <span :id="`cally-${todo.id}`">{{
              todo.date === "" ? "Set Date" : todo.date
            }}</span>
            <img
              src="../../assets/img/icon/calendar.svg"
              class="w-[16px] h-[16px] opacity-60"
            />
          </button>
          <div
            popover
            :id="`cally-popover-${todo.id}`"
            class="dropdown bg-white rounded-md border border-gray-500 shadow-lg mt-1 custom-calendar-popup"
            :style="{ 'position-anchor': `--cally-${todo.id}` }"
          >
            <calendar-date
              class="cally"
              @change="handleChangeDate($event, todo)"
            >
              <svg
                aria-label="Previous"
                class="fill-gray-500 size-4 hover:bg-transparent"
                slot="previous"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path d="M15.75 19.5 8.25 12l7.5-7.5"></path>
              </svg>
              <svg
                aria-label="Next"
                class="fill-gray-500 size-4"
                slot="next"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path d="m8.25 4.5 7.5 7.5-7.5 7.5"></path>
              </svg>
              <calendar-month></calendar-month>
            </calendar-date>
          </div>
        </div>
      </div>
      <div v-if="todo.isOpen" class="flex gap-3 text-gray-700">
        <div class="h-[20px] w-[20px] mt-1 cursor-pointer" @click="toggleEdit(todo)">
          <img
            src="../../assets/img/icon/pen.svg"
            class="h-[15px] w-[15px] mt-1"
            :class="{ grayscale: todo.description === '' }"
          />
        </div>
        <div v-if="!todo.isEdit" class="w-md" @click="toggleEdit(todo)">
          {{ todo.description === "" ? "No Description" : todo.description }}
        </div>
        <textarea
          v-if="todo.isEdit"
          v-model="todo.description"
          cols="4"
          rows="3"
          class="w-md border border-gray-500 rounded p-2 outline-none text-gray-700"
          placeholder="No Description"
        >
          No Description
        </textarea>
      </div>
    </div>
  </section>
</template>

<style scoped>
textarea {
  resize: none;
}

.custom-calendar-popup {
  transform: scale(0.85) translate(110px, -24px);
}
</style>
