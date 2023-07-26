<template>
  <div>
    <base-header />
    <todo-input @addTodo="addTodo"/>
    <todo-list v-bind:propsdata="todoItems" @removeTodo="removeTodo"/>
    <todo-footer @clearAll="clearAll"/>
  </div>
</template>
<script>
import BaseHeader from "./components/BaseHeader.vue"
import TodoInput from "./components/TodoInput.vue"
import TodoList from "./components/TodoList.vue"
import TodoFooter from "./components/TodoFooter.vue"

export default {
  data() {
    return {
      todoItems: [],
    }
  },
  methods: {
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem)
      this.todoItems.push(todoItem)
    },
    removeTodo(todoItem, index){
      localStorage.removeItem(localStorage.key(index));
      this.todoItems.splice(index, 1)
    },
    clearAll() {
      localStorage.clear()
      this.todoItems = []
    }
  },

  created() {
    if (localStorage.length > 0) {
      for(let i = 0 ; i < localStorage.length ; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  components: {
    "base-header": BaseHeader,
    "TodoInput" : TodoInput,
    "TodoList" : TodoList,
    "TodoFooter" : TodoFooter
  }
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