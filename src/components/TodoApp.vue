<template>
  <h1>Todo List</h1>
  <form @submit.prevent="addNewTodo">
    <input v-model="newTodo" name="newTodo">
    <button>Add</button>
  </form>
  <div v-for="todo in todos" :key="todo.id" class="todo">
    <input type=checkbox  @click="toggleDone(todo)" >
    <span :class="{ done: todo.done }">{{todo.content}}</span>
  </div>
  <button @click="removeAllTodos">clear</button>
</template>

<script>
import { ref } from 'vue';
export default {
  name: 'TodoApp',
  setup() {
    const newTodo = ref('');
    const todos = ref([]);
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }
    function toggleDone(todo) {
      todo.done = !todo.done;
    }
    function removeAllTodos() {
      todos.value = [];
    }
    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeAllTodos,
    };
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>