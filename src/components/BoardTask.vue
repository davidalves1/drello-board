<script setup lang="ts">
  import { computed } from 'vue'

  import DragHandle from './DragHandle.vue'
  import type { Task } from '../types'

  const { task } = defineProps<{
    task: Task
  }>()

  const createdAt = computed(() =>
    new Intl.DateTimeFormat('en-GB', { dateStyle: 'short' }).format(
      task.createdAt || Date.now(),
    ),
  )
</script>
<template>
  <div
    :title="createdAt"
    class="task bg-white px-1 py-2 rounded shadow-sm max-w-60 flex"
  >
    <DragHandle :width="18" :height="18" class="pr-2 pt-[2px]" />
    <span>{{ task.title }}</span>
  </div>
</template>

<style>
  .sortable-drag .task {
    transform: rotate(3deg);
  }

  .sortable-ghost .task {
    position: relative;
  }

  .sortable-ghost .task::after {
    content: '';
    @apply absolute top-0 bottom-0 left-0 right-0 bg-gray-200 shadow-none;
  }
</style>
