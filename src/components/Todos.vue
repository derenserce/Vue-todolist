<template>
  <div
    className="min-h-screen bg-gradient-to-b from-teal-500 to-blue-500 flex items-center justify-center">
    <div className="bg-white shadow-lg shadow-gray-900 rounded-sm p-4">
      <h1 class="font-bold text-2xl">Todo's App</h1>

      <!--Input-->
      <TodoInput
        :addTodo="addTodo"
        :newTodo="newTodo"
        @update:newTodo="updateNewTodo" />

      <!--List-->
      <TodoList
        :todos="todos"
        :deleteTodo="deleteTodo"
        :clearTodos="clearTodos" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import TodoList from "./TodoList.vue";
import TodoInput from "./TodoInput.vue";

const todos = ref([]);

const newTodo = ref("");
const updateNewTodo = (value) => {
  newTodo.value = value;
};

onMounted(() => {
  const storedTodos = localStorage.getItem("todos");
  if (storedTodos) {
    todos.value = JSON.parse(storedTodos);
  }
});

const addTodo = () => {
  if (newTodo.value.trim() !== "") {
    todos.value.push(newTodo.value.trim());
    newTodo.value = "";

    localStorage.setItem("todos", JSON.stringify(todos.value));
  }
};

const clearTodos = () => {
  todos.value = [];

  localStorage.removeItem("todos");
};

const deleteTodo = (index) => {
  todos.value.splice(index, 1);
  localStorage.removeItem("todos", JSON.stringify(todos.value));
};
</script>
