<script setup lang="ts">
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import type { Task } from "./types.ts";

const title = ref("Tasks App");
const taskArr = ref<Task[]>([]);

function addTask(newTask: string) {
  taskArr.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
}
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm @add-task="addTask" />
  </main>
</template>

<style>
main {
  max-width: 800px;
  margin: 1rem auto;
}
.button-container {
  display: flex;
  justify-content: end;
}
</style>
