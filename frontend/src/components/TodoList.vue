<template>
  <q-list class="column items-center">
    <q-item v-ripple :key="index" v-for="(todo, index) in todoItems" style= "width: 700px; " class="q-mt-xs">
      <q-item-section avatar>
        <q-icon color="primary" name="bluetooth" />
      </q-item-section>
      <q-item-section>{{todo}}</q-item-section>
      <q-icon color="primary" name="clear" @click="removeTodo" :index="index" />
    </q-item>
  </q-list>
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

