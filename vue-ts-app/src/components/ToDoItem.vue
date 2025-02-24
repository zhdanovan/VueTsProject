<template>
  <li></li>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

interface Todo {
  text: string;
  completed: boolean;
}

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