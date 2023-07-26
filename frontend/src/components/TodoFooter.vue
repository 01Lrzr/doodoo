<template>
  <div>
    <button @click="clearAll">clear</button>
  </div>
</template>
<script>
  export default {
    methods : {
      clearAll() {
        this.$emit('clearAll')
      }
    }
  }
</script>
