<template>
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
  <div class="mt-6 flex justify-between gap-4 items-center">
    <p>Amount of tasks remaining: {{ todos.length }}</p>
    <button
      class="bg-purple-500 text-white px-2 py-1 rounded"
      @click="clearTodos">
      Clear all
    </button>
  </div>
</template>

<script setup>
defineProps({
  todos: Array,
  deleteTodo: Function,
  clearTodos: Function,
});
</script>
