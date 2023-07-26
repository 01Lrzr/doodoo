<template>
  <div>
    <BaseHeader />
    <TodoInput @addTodo="addTodo"/>
    <TodoList v-bind:todoItems="todoItems" @removeTodo="removeTodo"/>
    <TodoFooter @clearAll="clearAll"/>
  </div>
</template>
<script setup>
import BaseHeader from "./components/BaseHeader.vue"
import TodoInput from "./components/TodoInput.vue"
import TodoList from "./components/TodoList.vue"
import TodoFooter from "./components/TodoFooter.vue"
import { ref } from "vue"

const todoItems = ref([]);

if (localStorage.length > 0) {
  for(let i = 0 ; i < localStorage.length ; i++) {
    todoItems.value.push(localStorage.key(i));
  }
}

function addTodo(todoItem) {
  localStorage.setItem(todoItem, todoItem)
  todoItems.value.push(todoItem)
}

function removeTodo(index){
  localStorage.removeItem(localStorage.key(index));
  todoItems.value.splice(index, 1)
}

function clearAll() {
  localStorage.clear()
  todoItems.value = []
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>