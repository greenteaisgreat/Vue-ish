<script setup lang="ts">
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";

const title = ref("Tasks App");
const taskArr = ref([]);
let id = 0;

function addTask(newTask: string) {
  console.log({ newTask });
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
