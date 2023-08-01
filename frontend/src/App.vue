<template>
  <div>
    <BaseHeader />
    <TodoInput @addTodo="addTodo"/>
    <TodoList  v-bind:todoItems="todoItems" @removeTodo="removeTodo" @selectDay="selectDay"/>
    <TodoFooter @clearAll="clearAll"/>
  </div>
</template>
<script setup>
import BaseHeader from "./components/BaseHeader.vue"
import TodoInput from "./components/TodoInput.vue"
import TodoList from "./components/TodoList.vue"
import TodoFooter from "./components/TodoFooter.vue"
import { ref } from "vue"

const todoItems = ref([[], [], [], [], [], [], []]);
let day = 0;

function addTodo(todoItem) {
  todoItems.value[day].push(todoItem)
}

function removeTodo(index){
  todoItems.value[day].splice(index, 1)
}

function clearAll() {
  todoItems.value = [[], [], [], [], [], [], []];
}

function selectDay(i) {
  day = i;
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