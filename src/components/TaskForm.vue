<script lang="ts" setup>
import { ref } from "vue";

const newTask = ref("");
const emit = defineEmits<{
  addTask: [newTask: string];
}>();

function formSubmitted() {
  console.log(newTask.value);

  emit("addTask", newTask.value);
  newTask.value = "";
}
</script>

<template>
  <form @submit.prevent="formSubmitted">
    <label for="newTask">
      New Task
      <input name="newTask" v-model="newTask" />
    </label>
    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>
