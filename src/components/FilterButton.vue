<script lang="ts" setup>
import type { TaskFilter } from "@/types";

const props = defineProps<{
  filter: TaskFilter;
  currentFilter: TaskFilter;
}>();

const emit = defineEmits<{
  setFilter: [filterType: TaskFilter];
}>();
</script>

<template>
  <button
    @click="emit('setFilter', props.filter)"
    class="secondary"
    :class="{ contrast: props.currentFilter === props.filter }"
  >
    {{ props.filter }}
  </button>
</template>

<style scoped>
button {
  text-transform: capitalize;
}
</style>
