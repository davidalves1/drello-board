<script setup lang="ts">
  import { ref } from "vue";
  import draggable from "vuedraggable";

  import type { Column, Task } from "../types";

  import BoardTask from "./BoardTask.vue";
  import DragHandle from "./DragHandle.vue";

  const fakeColumns = [
    {
      id: crypto.randomUUID(),
      title: "Ready for development",
      tasks: [
        {
          id: crypto.randomUUID(),
          title: "Create task component",
          createdAt: new Date(),
        },
        {
          id: crypto.randomUUID(),
          title: "Create add new task component",
          createdAt: new Date(),
        },
      ],
    },
    {
      id: crypto.randomUUID(),
      title: "In progress",
      tasks: [
        {
          id: crypto.randomUUID(),
          title: "Create board component",
          createdAt: new Date(),
        },
      ],
    },
    {
      id: crypto.randomUUID(),
      title: "Done",
      tasks: [],
    },
  ];

  const columns = ref<Column[]>(fakeColumns as Column[]);
</script>
<template>
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      :animation="150"
      handle=".drag-handle"
      class="flex gap-3 overflow-x-auto items-start"
    >
      <template #item="{ element: column }: { element: Column }">
        <div
          class="column flex flex-col bg-zinc-100 p-3 rounded min-w-60 gap-2"
        >
          <header class="font-bold mb-2 flex items-center">
            <DragHandle :width="18" :height="18" />
            {{ column.title }}
          </header>
          <draggable
            v-model="column.tasks"
            group="tasks"
            item-key="id"
            :animation="150"
            handle=".drag-handle"
            class="flex flex-col gap-3"
          >
            <template #item="{ element: task }: { element: Task }">
              <BoardTask :task="task" class="flex-1" />
            </template>
          </draggable>
          <footer>
            <button class="text-gray-500 mt-1">+ Add a Task</button>
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>
