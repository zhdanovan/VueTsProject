<template>
  <li :class="{completed : todo.completed}">
    <input type = "checkbox" v-model="todo.completed"/>
    <strong>{{ todo.text }}</strong>
    <button @click="deleteTodo">Delete Task</button>
  </li>
</template>

<script lang="ts">
import { defineComponent, type PropType } from 'vue';
import { type Todo } from '../types/todo';

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    },
  },
  methods: {
    deleteTodo() {
      this.$emit('remove', this.todo);
    },
  },
});
</script>

<style scoped>
</style>