<script setup lang="ts">
  import type { Task } from "../types";
  import DragHandle from "./DragHandle.vue";

  const { task } = defineProps<{
    task: Task;
  }>();
</script>
<template>
  <div
    :title="task.createdAt.toLocaleDateString()"
    class="task bg-white px-1 py-2 rounded shadow-sm max-w-60 flex"
  >
    <DragHandle :width="18" :height="18" class="pr-2 pt-[2px]" />
    <span>{{ task.title }}</span>
  </div>
</template>
