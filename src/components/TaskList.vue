<script lang="ts" setup>
import type { Task } from "@/types";

const props = defineProps<{
  tasks: Task[];
}>();
const emit = defineEmits<{
  toggleDone: [id: string];
  removeTask: [id: string];
}>();
</script>

<template>
  <!-- in picoCSS, articles are automatically stylized cards -->
  <TransitionGroup name="list" tag="div" class="task-list">
    <article v-for="task in props.tasks" :key="task.id" class="task">
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
      <!--class outline is picoCSS-->
      <button class="outline" @click="emit('removeTask', task.id)">
        Remove
      </button>
    </article>
  </TransitionGroup>
</template>

<style>
.task-list {
  margin-top: 1rem;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.done {
  text-decoration: line-through;
}

/* apply transition to moving elements*/
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(300px);
}

/* helps animated remaining items*/
.list-leave-active {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: absolute;
}
</style>
