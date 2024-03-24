<script setup lang="ts">
  import Board from './components/Board.vue'
  import icon from './assets/drello-board.svg'
</script>

<template>
  <div class="p-10 h-[100vh] bg-teal-600 overflow-auto">
    <h1 class="flex items-end gap-1 text-4xl text-white mb-8">
      <img :src="icon" width="40" />
      Drello Board
    </h1>
    <Board />
  </div>
</template>
