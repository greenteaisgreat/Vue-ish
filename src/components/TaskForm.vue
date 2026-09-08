<script lang="ts" setup>
import { ref } from "vue";

const newTask = ref("");
const emit = defineEmits<{
  addTask: [newTask: string];
}>();

function formSubmitted() {
  // trim prevents a bunch of spaces from being entered
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value = "";
  }
}
</script>

<template>
  <form @submit.prevent="formSubmitted">
    <label for="newTask">
      New Task
      <input
        name="newTask"
        v-model="newTask"
        required
        pattern="\w{0,999}"
        title="Task cannot be empty!"
      />
    </label>
    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>
