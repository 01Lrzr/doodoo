<template>
  <div>
   <input type="text" v-model="newTodo" @keyup.enter="addTodo">
   <button @click="addTodo">+</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      newTodo: '',
    }
  },
  methods: {
    addTodo(){
      if (this.newTodo !== "") {
        const value = this.newTodo && this.newTodo.trim();
        this.$emit('addTodo', value)
        this.newTodo = "";
      }
    }
  }
}

</script>