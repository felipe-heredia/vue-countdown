<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <h1 class="title">Contador</h1>
  <RouterView />
</template>

<style>
@import '@/assets/base.css';

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  height: 100vh;
  padding-bottom: 5rem;

  font-weight: normal;
}

h1.title {
  font-weight: 700;
  font-size: 4rem;
  line-height: 3.7rem;
}
</style>
