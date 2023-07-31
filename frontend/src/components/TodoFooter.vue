<template>
  <div>
    <q-btn :ripple="{ center: true }" no-caps outline color="primary" label="clear" @click="clearAll" />
  </div>
</template>
<script setup>
  import { defineEmits } from "vue"
  
  const emit = defineEmits(['clearAll'])
  function clearAll() {
    emit('clearAll')
  }
</script>
