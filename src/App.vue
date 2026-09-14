<script setup lang="ts">
import { ref, computed } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import type { Task } from "./types.ts";

const title = ref("Tasks App");
const tasks = ref<Task[]>([]);

const totalDone = computed(() =>
  tasks.value.reduce((total, task) => (task.done ? total + 1 : total), 0),
);

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
}
function toggleDone(id: string) {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.done = !task.done;
  }
}
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm @add-task="addTask" />
    <h3 v-if="!tasks.length">Add a Task to Get Started</h3>
    <h3 v-else>{{ totalDone }}/{{ tasks.length }} Tasks Completed</h3>
    <!-- syntactic sugar for :tasks="tasks" -->
    <TaskList :tasks @toggle-done="toggleDone" />
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
