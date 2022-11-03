<script setup>
import Recetas from './components/Recetas.vue'
</script>

<template>
  <div class="app">
    <h1 class="title">Buscador Pokemon</h1>
    <Recetas />
  </div>
</template>

<style scoped>
.title {
  color: var(--color);
  text-align: center;
}

.app {}
</style>
