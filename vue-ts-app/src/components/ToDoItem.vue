<template>
  <li :class="{completed : todo.completed,  editing: isEditing}">
    <div v-if="!isEditing" class="view">
      <input type="checkbox" v-model="todo.completed" />
      <span @dblclick="startEditing">{{ todo.text }}</span>
      <button @click="deleteTodo(todo)">Удалить</button>
    </div>
    <input
      v-else
      type="text"
      :value="todo.text"
      @input="updateText"
      @keyup.enter="finishEditing"
      @keyup.esc="cancelEditing"
      @blur="finishEditing"
      class="edit"
    />
  </li>
</template>

<script lang="ts">
import { defineComponent, type PropType, ref } from 'vue';
import { type Todo } from '../types/todo';

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    },
    isEditing: {
      type: Boolean,
      required: true,
    },
  },
  emits: ['delete', 'edit'],
  setup(props, { emit }) {
    const editedText = ref(props.todo.text); 
    const startEditing = () => {
      emit('edit', props.todo, null); 
    };

    const updateText = (event: Event) => {
      editedText.value = (event.target as HTMLInputElement).value;
    };

    const finishEditing = () => {
      emit('edit', props.todo, editedText.value); 
    };

    const cancelEditing = () => {
      emit('edit', props.todo, null); 
    };

    const deleteTodo = (todo: Todo) => {
      emit('delete', todo);
    };
    return {
      startEditing,
      updateText,
      finishEditing,
      cancelEditing,
      deleteTodo,
    };
  },
});
</script>

<style scoped>
</style>