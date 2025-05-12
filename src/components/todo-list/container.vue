<script setup>
import { reactive, ref } from "vue";
import TodoCard from "./card.vue";
import { uuid } from "vue-uuid";
import { todoItem } from "../../constants";

const todo = reactive({
  data: [
    {
      id: uuid.v4(),
      title:
        "Set up documentation report for several Cases : Case 145443, Case 192829 and Case 182203",
      createdAt: "12/04/2025",
      date: "12/05/2025",
      description:
        "Closing off this case since this application has been cancelled. No one really understand how this case could possibly be cancelled. The options and the documents within this document were totally a guaranteed for a success!",
      checked: false,
      isOpen: false,
      isEdit: false,
      remaining: 0,
    },
  ],
});

const getToday = () => {
  var today = new Date();
  var dd = String(today.getDate()).padStart(2, "0");
  var mm = String(today.getMonth() + 1).padStart(2, "0");
  var yyyy = today.getFullYear();

  return dd + "/" + mm + "/" + yyyy;
};

const addTodo = () => {
  const todayDate = getToday();
  let newTodo = {};
  Object.assign(newTodo, todoItem);
  newTodo.id = uuid.v4();
  newTodo.createdAt = todayDate;
  newTodo.isEdit = true;
  todo.data.push(newTodo);
};

const deleteTodo = (id) => {
  const newTasks = todo.data.filter((todo) => todo.id !== id);
  todo.data = newTasks;
};
</script>

<template>
  <section>
    <div
      class="sticky top-0 bg-white h-full pt-4.5 pb-5 flex items-center justify-between px-2 z-10"
    >
      <div className="dropdown">
        <div
          tabIndex="{0}"
          role="button"
          className="btn m-1 bg-white shadow-none border border-gray-500 text-gray-600 font-semibold px-3.5 py-2.5 flex justify-between"
        >
          My tasks
          <img
            src="../../assets/img/icon/chevron-down.svg"
            class="h-[20px] w-[20px]"
          />
        </div>
        <ul
          tabIndex="{0}"
          className="dropdown-content menu rounded-box z-1 w-52 p-0 shadow-sm bg-white border border-gray-500 text-gray-600 "
        >
          <li class="border-b border-gray-500 font-semibold p-0">
            <a>Personal Errands</a>
          </li>
          <li class="font-semibold p-0"><a>Urgent To-Do</a></li>
        </ul>
      </div>
      <button
        @click="addTodo()"
        className="btn bg-[#2F80ED] border-0 shadow-none px-4 py-3.5"
      >
        New Task
      </button>
    </div>
    <div class="min-h-[400px] pl-7 pr-2.5 todos-card">
      <TodoCard
        v-for="todo in todo.data"
        :key="todo.id"
        :todo="todo"
        @delete-todo="deleteTodo"
      />
    </div>
  </section>
</template>

<style scoped>
.todos-card {
  height: calc(100% - 4000px);
}
</style>