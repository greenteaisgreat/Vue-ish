<script lang="ts" setup>
import type { Task } from "@/types";

const props = defineProps<{
  tasks: Task[];
}>();
const emit = defineEmits<{
  toggleDone: [id: string];
}>();
</script>

<template>
  <div class="task-list">
    <!-- in picoCSS, articles are automatically stylized cards -->
    <article v-for="task in props.tasks" :key="task.id">
      <label>
        <!-- v-model considered an anti-pattern, since it's modifying state 
        defined elsewhere, in this case, the parent -->
        <!-- <input v-model="task.done" type="checkbox" /> -->
        <input
          type="checkbox"
          @input="emit('toggleDone', task.id)"
          :checked="task.done"
        />
        <span :class="{ done: task.done }">{{ task.title }}</span>
      </label>
    </article>
  </div>
</template>

<style>
.task-list {
  margin-top: 1rem;
}

.done {
  text-decoration: line-through;
}
</style>
