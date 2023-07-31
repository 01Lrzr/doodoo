<template>
  <div>
    <BaseHeader />
    <TodoInput @addTodo="addTodo"/>
    <div class="wrap">
     <div class="container">
       <q-card flat bordered class="my-card" :key="day" v-for="(day, index) in week" :index="index">
          <!-- <q-card-section> -->
            <div :index="index"  @click="selectDay" class="text-h6 day" >{{day}}</div>
          <!-- </q-card-section> -->
          <q-separator inset />
          <q-card-section class="q-pt-none">
          <TodoList :index="index" v-bind:todoItems="todoItems[index]" @removeTodo="removeTodo"/>
          </q-card-section>
        </q-card>
      </div>
    </div>
    <TodoFooter @clearAll="clearAll"/>
  </div>
</template>
<script setup>
import BaseHeader from "./components/BaseHeader.vue"
import TodoInput from "./components/TodoInput.vue"
import TodoList from "./components/TodoList.vue"
import TodoFooter from "./components/TodoFooter.vue"
import { ref, onMounted } from "vue"

// eslint-disable-next-line
const todoItems = ref(Array.from(Array(7), () => new Array()));
const week= [ "월요일", "화요일", "수요일", "목요일", "금요일", "토요일", "일요일"];
let day = 0;

onMounted(() => {
  document.querySelector('.day').classList.add('selected');
})

function addTodo(todoItem) {
  todoItems.value[day].push(todoItem)
}

function removeTodo(index){
  todoItems.value[day].splice(index, 1)
}

function clearAll() {
  // eslint-disable-next-line
  todoItems.value = Array.from(Array(7), () => new Array());
}

function selectDay(e) {
  day = e.target.getAttribute('index');
  if ( document.querySelector('.selected') ) {
    document.querySelector('.selected').classList.remove('selected');
  }
  e.target.classList.add('selected')
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

.container {
  display: flex;
  flex-wrap: wrap; 
  gap: 5px 5px;
  margin:0 auto; 

    .my-card {
      width: 20%;
      height : 300px;
      
      .selected {
        background-color: $primary;
        color : white;
      }
    }
}


.wrap {
  margin: 0 auto;
}
</style>