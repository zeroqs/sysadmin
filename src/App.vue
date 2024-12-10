<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <header class="header"><RouterLink to="/">Home</RouterLink></header>

  <RouterView />
</template>

<style scoped>
.header {
  padding: 10px 0px;
  font-size: 16px;

  a {
    transition: all 0.3s ease-in-out;

    &:hover {
      cursor: pointer;
      color: #42b883;
    }
  }
}
</style>
