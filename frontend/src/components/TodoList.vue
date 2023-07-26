<template>
  <ul>
    <li :key="index" v-for="(todo, index) in todoItems">
    {{todo}}
    <button @click="removeTodo" :index="index">x</button>
    </li>
  </ul>
</template>

<script setup>
  import { defineProps, defineEmits } from 'vue'

  const props = defineProps(['todoItems'])
  const emit = defineEmits(['removeTodo'])

  function removeTodo(e) {
    const index = e.target.getAttribute('index')
    emit('removeTodo', index)
  }
</script>

