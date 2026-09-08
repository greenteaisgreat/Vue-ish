<script lang="ts" setup>
import type { Task } from "@/types";

const props = defineProps<{
  taskArr: Task[];
}>();
</script>

<template>
  <!-- in picoCSS, articles are automatically stylized cards -->
  <article v-for="task in props.taskArr" :key="task.id">
    {{ task.title }}
  </article>
</template>
