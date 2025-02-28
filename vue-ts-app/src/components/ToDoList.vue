<template>
    <div>
      <ul>
        <TodoItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @remove="removeTodo"
        />
      </ul>
      <input v-model="newTodoText" @keyup.enter="addTodo" placeholder="AddTask" />
    </div>
  </template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import TodoItem from './ToDoItem.vue';
import { type Todo } from '../types/todo';


export default defineComponent({
  components: {
    TodoItem,
  },
  setup() {
    const todos = ref<Todo[]>([]);
    const newTodoText = ref('');
    let nextTodoId = 1;

    const addTodo = () => {
      if (newTodoText.value.trim() === '') return;
      todos.value.push({
        id:nextTodoId++,
        text: newTodoText.value,
        completed: false,
      });
      newTodoText.value = '';
    };

    const removeTodo = (todo: Todo) => {
      todos.value = todos.value.filter((t) => t !== todo);
    };

    return {
      todos,
      newTodoText,
      addTodo,
      removeTodo,
    };
  },
});
</script>