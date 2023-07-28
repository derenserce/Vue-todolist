<script setup>
import { ref, onMounted } from "vue";

defineProps({
  msg: String,
});

const todos = ref([]);

const addedTodo = ref("");

onMounted(() => {
  // Retrieve todos from localStorage when the component is mounted
  const storedTodos = localStorage.getItem("todos");
  if (storedTodos) {
    todos.value = JSON.parse(storedTodos);
  }
});

const addTodo = () => {
  if (addedTodo.value.trim() !== "") {
    todos.value.push(addedTodo.value.trim());
    addedTodo.value = "";

    localStorage.setItem("todos", JSON.stringify(todos.value));
  }
};

const clearTodos = () => {
  todos.value = [];

  localStorage.removeItem("todos");
};

const deleteTodo = (index) => {
  todos.value.splice(index, 1);
  localStorage.setItem("todos", JSON.stringify(todos.value));
};
</script>

<template>
  <div
    className="min-h-screen bg-gradient-to-b from-teal-500 to-blue-500 flex items-center justify-center">
    <div className="bg-white shadow-lg shadow-gray-900 rounded-sm p-4">
      <h1 class="font-bold text-2xl">Todo App</h1>

      <!--Input-->
      <div class="mt-2">
        <form @submit.prevent="addTodo" class="flex gap-4 justify-between">
          <input
            type="text"
            v-model="addedTodo"
            placeholder="Add your new todo"
            class="border-[1px] py-2 px-3 w-full" />
          <button
            type="submit"
            class="bg-purple-500 text-white text-4xl text-center px-3 pb-2 rounded">
            +
          </button>
        </form>
      </div>

      <!--List-->
      <div>
        <ul class="flex flex-col gap-4 mt-4">
          <li
            v-for="(todo, index) in todos"
            :key="index"
            class="bg-gray-200 py-2 px-3 text-lg capitalize rounded flex items-center justify-between gap-4">
            <span>{{ todo }}</span>
            <button
              class="bg-red-500 text-white py-2 px-4 rounded"
              @click="deleteTodo(index)">
              -
            </button>
          </li>
        </ul>
      </div>

      <!--Amount-->
      <div class="mt-6 flex justify-between">
        <p>Amount of tasks remaining: {{ todos.length }}</p>
        <button
          class="bg-purple-500 text-white px-2 py-1 rounded"
          @click="clearTodos">
          Clear all
        </button>
      </div>
    </div>
  </div>
</template>
