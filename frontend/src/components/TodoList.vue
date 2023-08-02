<template>
<div class="wrap">
  <div class="container">
    <q-card flat bordered class="my-card" :key="day" v-for="(day, index) in week" :index="index">
      <q-card-section :index="index" @click="selectDay(index)" class="text-h6" :class="{'selected': index === selected}">
        {{ day }}
      </q-card-section>
      <q-separator inset />
      <q-card-section class="q-pt-none">

      <q-list class="column items-center">
        <q-item v-ripple :key="i" v-for="(todo, i) in todoItems[index]" class="q-mt-xs">
          <q-item-section>{{todo}}</q-item-section>
          <q-icon color="primary" name="clear" @click="removeTodo(day, i)" :index="i" />
        </q-item>
      </q-list>

      </q-card-section>
    </q-card>
  </div>
</div>
</template>

<script setup>
  import { onMounted, defineProps, defineEmits, ref } from 'vue'
  const props = defineProps(['todoItems'])
  const emit = defineEmits(['removeTodo', 'selectDay'])
  const week= [ "월요일", "화요일", "수요일", "목요일", "금요일", "토요일", "일요일"];
  const selected = ref(0);

  function removeTodo(day, index) {
    const dayIdx = week.indexOf(day)
    emit('removeTodo', dayIdx, index)
  }

  function selectDay(index) {
    selected.value = index
    emit('selectDay', selected.value)
  }

</script>
<style lang="scss">
.wrap {
  margin: 0 auto;
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
}
</style>