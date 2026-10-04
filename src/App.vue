<script setup lang="ts">
import { ref, computed } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import FilterButton from "./components/FilterButton.vue";
import type { Task, TaskFilter } from "./types.ts";

const title = ref("Tasks App");
const tasks = ref<Task[]>([]);
const filter = ref<TaskFilter>("all");

// similar to useMemo in react; it only runs if one its dependencies change.
// computed is used to alter existing reactive data
const totalDone = computed(() =>
  tasks.value.reduce((total, task) => (task.done ? total + 1 : total), 0),
);

const filterTasks = computed(() => {
  switch (filter.value) {
    case "all":
      return tasks.value;
    case "done":
      return tasks.value.filter((task) => task.done);
    case "todo":
      return tasks.value.filter((task) => !task.done);
  }
  return tasks.value;
});

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
}

function removeTask(id: string) {
  tasks.value = tasks.value.filter((task) => task.id !== id);
}

function toggleDone(id: string) {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.done = !task.done;
  }
}

function setFilter(filterType: TaskFilter) {
  filter.value = filterType;
}
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm @add-task="addTask" />
    <h3 v-if="!tasks.length">Add a Task to Get Started</h3>
    <h3 v-else>{{ totalDone }}/{{ tasks.length }} Tasks Completed</h3>
    <div v-if="tasks.length" class="button-container">
      <FilterButton
        :currentFilter="filter"
        filter="all"
        @set-filter="setFilter('all')"
      />
      <FilterButton
        :currentFilter="filter"
        filter="todo"
        @set-filter="setFilter('todo')"
      />
      <FilterButton
        :currentFilter="filter"
        filter="done"
        @set-filter="setFilter('done')"
      />
    </div>
    <!-- syntactic sugar for :tasks="tasks", used to be just :tasks before 'filterTasks' -->
    <TaskList
      :tasks="filterTasks"
      @toggle-done="toggleDone"
      @remove-task="removeTask"
    />
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
  gap: 1rem;
}
</style>
