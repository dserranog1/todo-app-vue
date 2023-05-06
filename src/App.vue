<script setup lang="ts">
import TodoComponent from "./components/TodoComponent.vue";
</script>

<template>
  <div
    class="w-full flex flex-col justify-center items-center my-auto h-full min-h-screen bg-gray-200 text-2xl py-6 text-gray-600"
  >
    <div class="flex flex-col items-center gap-4">
      <h1>Todo App</h1>
      <h2 class="text-lg">Click any todo to edit it (when unchecked)</h2>
    </div>
    <TodoComponent />
  </div>
</template>
