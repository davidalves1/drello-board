<script setup lang="ts">
  import { ref } from 'vue'
  import draggable from 'vuedraggable'

  import type { Column, Task } from '../types'

  import BoardTask from './BoardTask.vue'
  import DragHandle from './DragHandle.vue'
  import { useKeyModifier } from '@vueuse/core'

  const fakeColumns = [
    {
      id: crypto.randomUUID(),
      title: 'Ready for development',
      tasks: [
        {
          id: crypto.randomUUID(),
          title: 'Create task component',
          createdAt: new Date(),
        },
        {
          id: crypto.randomUUID(),
          title: 'Create add new task component',
          createdAt: new Date(),
        },
      ],
    },
    {
      id: crypto.randomUUID(),
      title: 'In progress',
      tasks: [
        {
          id: crypto.randomUUID(),
          title: 'Create board component',
          createdAt: new Date(),
        },
      ],
    },
    {
      id: crypto.randomUUID(),
      title: 'Done',
      tasks: [],
    },
  ]

  const columns = ref<Column[]>(fakeColumns as Column[])

  const alt = useKeyModifier('Alt')
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
          <!-- https://sortablejs.github.io/Sortable/#cloning -->
          <draggable
            v-model="column.tasks"
            :group="{ name: 'tasks', pull: alt ? 'clone' : true }"
            item-key="id"
            :animation="150"
            handle=".drag-handle"
            class="flex flex-col gap-3"
          >
            <template #item="{ element: task }: { element: Task }">
              <div>
                <BoardTask :task="task" class="flex-1" />
              </div>
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
