<template>
  <div>
   <input type="text" v-model="newTodo" @keyup.enter="addTodo">
   <button @click="addTodo">+</button>
  </div>
</template>
<script setup>
  import { ref, defineEmits } from "vue"

  const newTodo = ref('')
  const emit = defineEmits(['addTodo'])

  function addTodo() {
    if (newTodo.value !== "") {
      emit('addTodo', newTodo.value)
      newTodo.value = ''
    }
  }

</script>