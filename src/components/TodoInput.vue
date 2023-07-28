<template>
  <div class="mt-2">
    <form @submit.prevent="addTodo" class="flex gap-4 justify-between">
      <input
        type="text"
        v-bind:value="newTodo"
        @input="$emit('update:newTodo', $event.target.value)"
        placeholder="Add your new todo"
        class="border-[1px] py-2 px-3 w-full" />
      <button
        type="submit"
        class="bg-purple-500 text-white text-4xl text-center px-3 pb-2 rounded">
        +
      </button>
    </form>
  </div>
</template>

<script setup>
defineProps({
  addTodo: Function,
  newTodo: String,
  updateAddedTodo: Function,
});
</script>
