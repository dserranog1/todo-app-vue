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
  todoList.value.push(newTodo);
};

const deleteTodo = (id: string) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== id);
};
</script>

<template>
  <div
    class="flex flex-col items-center justify-center flex-1 w-full h-full my-10"
  >
    <div v-if="todoList.length > 0">
      <div
        :key="todo.id"
        v-for="todo in todoList"
        class="flex flex-row gap-6 relative my-4"
      >
        <button
          class="px-3 absolute -left-16 top-1"
          @click="deleteTodo(todo.id)"
        >
          <img src="../assets/x.svg" alt="" />
        </button>
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
    </div>
    <div v-else>So empty...</div>
    <button
      @click="createTodo"
      class="text-lg rounded-md bg-green-200 hover:bg-green-300 p-2 my-6"
    >
      Add new
    </button>
  </div>
</template>
