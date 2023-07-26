<template>
  <ul>
    <li :key="index" v-for="(todo, index) in propsdata">
    {{todo}}
    <button @click="removeTodo" :index="index">x</button>
    </li>
  </ul>
</template>

<script >
export default{
  props: ['propsdata'],

  methods : {
    removeTodo(todoItem, index) {
      this.$emit('removeTodo', todoItem, index)
    }
  }
};
</script>

