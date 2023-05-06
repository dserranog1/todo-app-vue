<script setup lang="ts">
import { ref } from "vue";
import { Todo } from "../types";
import { v4 as uuidv4 } from "uuid";

const todoList = ref<Todo[]>([
  {
    id: uuidv4(),
    description: "Create Vue App",
    isDone: true,
    isEditing: false,
  },
]);

const createTodo = () => {
  const newTodo: Todo = {
    id: uuidv4(),
    description: "Click to edit me",
    isDone: false,
    isEditing: false,
  };
  todoList.value = [newTodo, ...todoList.value];
};
</script>

<template>
  <div
    class="flex flex-col items-center justify-center flex-1 w-full h-full gap-8 my-10"
  >
    <div :key="todo.id" v-for="todo in todoList" class="flex flex-row gap-6">
      <input
        class="w-6"
        v-model="todo.isDone"
        type="checkbox"
        :disabled="todo.isEditing"
      />
      <p
        v-if="!todo.isEditing"
        @click="todo.isEditing = todo.isDone ? false : !todo.isEditing"
      >
        <s v-if="todo.isDone">
          {{ todo.description }}
        </s>
        <span v-else>{{ todo.description }}</span>
      </p>
      <div v-else class="flex flex-row gap-4">
        <input
          type="text"
          v-model="todo.description"
          class="bg-gray-100 rounden-sm outline-none p-2"
        />
        <button
          class="text-sm rounded-sm bg-green-200 hover:bg-green-300 p-1"
          @click="todo.isEditing = false"
        >
          ok
        </button>
      </div>
    </div>
    <button
      @click="createTodo"
      class="text-lg rounded-md bg-green-200 hover:bg-green-300 p-2"
    >
      Add new
    </button>
  </div>
</template>
