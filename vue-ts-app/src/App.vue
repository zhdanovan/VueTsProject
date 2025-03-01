<template>
  <div id="app">
    <h1>VueTs - TodoList</h1>
    <ToDoList />
  </div>
</template>

<script setup lang="ts">
import ToDoList from './components/ToDoList.vue';
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
