<template>
  <h1> Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo"/>
    <button>Add New Todo</button>
  </form>
    <button @click="removeAll()">Remove All</button>
    <button @click="markAllDone()">Mall All Done</button>
  <ul>
    <li v-for="(todo, index)  in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="togleDone(todo)">{{todo.content}}</h3>
      <button @click="removeTodo(index)">Remove Todo</button>
    </li>
  </ul>
</template>

<script>

import { ref } from 'vue';

export default {
  setup() {
   /* const data = reactive({
      newTodo: '',
      todos: [],
    });*/
    const newTodo = ref('');
    const todos = ref([]);
    function addNewTodo() {
      todos.value.push( { 
        id: Date.now(),
        done: false,
        content: newTodo.value, }  );
        newTodo.value = '';
    }

    function togleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true );
    }

    function removeAll() {
      todos.value = [];
    }

  return {
    newTodo,
    todos,
    addNewTodo,
    togleDone,
    removeTodo,
    markAllDone,
    removeAll
  };

  }
}
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
  }
.todo{
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>
