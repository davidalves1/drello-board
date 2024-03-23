<script setup lang="ts">
  import { ref } from "vue";

  const source = ref("vite");
  console.log("teste");
</script>

<template>
  <h1>Hello {{ source }}!</h1>
</template>
