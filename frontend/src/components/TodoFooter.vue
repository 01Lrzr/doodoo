<template>
  <div>
    <button @click="clearAll">clear</button>
  </div>
</template>
<script setup>
  import { defineEmits } from "vue"
  
  const emit = defineEmits(['clearAll'])
  function clearAll() {
    emit('clearAll')
  }
</script>
