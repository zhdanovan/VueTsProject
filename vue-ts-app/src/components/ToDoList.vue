<template>
    <div>
      <ul>
        <TodoItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @delete="deleteTodo"
          @edit = "editTodo"
          :isEditing = "editTodoId === todo.id"
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
    const editTodoId = ref<number | null>(null);
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

    const deleteTodo = (todo: Todo) => {
      todos.value = todos.value.filter((t) => t !== todo);
    };

    const editTodo = (todo: Todo, newText:string) => {
      if (newText === null) {
        editTodoId.value = null;
      } else if (newText.trim()==='') {
        deleteTodo(todo);
      } else {
        todo.text = newText;
        editTodoId.value = null;
      }
    };

    return {
      todos,
      newTodoText,
      addTodo,
      deleteTodo,
      editTodoId,
      editTodo
    };
  },
});
</script>