<template>
  <div class="column items-center q-mt-md">
  <q-input rounded standout v-model="newTodo" @keyup.enter="addTodo" style= "width: 800px; ">
    <template v-slot:append>
      <q-btn round dense flat icon="add" @click="addTodo"/>
    </template>
  </q-input>
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