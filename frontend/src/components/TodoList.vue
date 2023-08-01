<template>
<div class="wrap">
  <div class="container">
    <q-card flat bordered class="my-card" :key="day" v-for="(day, index) in week" :index="index">
      <!-- <q-card-section> -->
        <div :index="index"  @click="selectDay" class="text-h6 day" >{{day}}</div>
      <!-- </q-card-section> -->
      <q-separator inset />
      <q-card-section class="q-pt-none">

      <q-list class="column items-center">
        <q-item v-ripple :key="i" v-for="(todo, i) in todoItems[index]" class="q-mt-xs">
          <!-- <q-item-section avatar>
            <q-icon color="primary" name="bluetooth" />
          </q-item-section> -->
          <q-item-section>{{todo}}</q-item-section>
          <q-icon color="primary" name="clear" @click="removeTodo" :index="i" />
        </q-item>
      </q-list>

      </q-card-section>
    </q-card>
  </div>
</div>
</template>

<script setup>
  import { onMounted, defineProps, defineEmits } from 'vue'
  const props = defineProps(['todoItems'])
  const emit = defineEmits(['removeTodo', 'selectDay'])
  const week= [ "월요일", "화요일", "수요일", "목요일", "금요일", "토요일", "일요일"];
  let day = 0;

  onMounted(() => {
    document.querySelector('.day').classList.add('selected');
  })

  function removeTodo(e) {
    const index = e.target.getAttribute('index')
    emit('removeTodo', index)
  }

  function selectDay(e) {
    day = e.target.getAttribute('index');
    if ( document.querySelector('.selected') ) {
      document.querySelector('.selected').classList.remove('selected');
    }
    e.target.classList.add('selected')
    emit('selectDay', day)
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