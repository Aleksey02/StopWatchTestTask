<template>
  <div class="main">
    <div class="container">
      <div class="main__box">
        <Stopwatch v-for="item in ids" :id="item" :key="ids" @deleteTimer="deleteTimer"></Stopwatch>
        <AddStopWatch @click="addStopWatch"></AddStopWatch>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Stopwatch from './components/Stopwatch.vue';
import AddStopWatch from './components/AddStopWatch.vue';

const ids = ref([0])

function addStopWatch(){
  if(ids.value.length>0){
    ids.value.push(ids.value[ids.value.length-1]+1)
  }else{
    ids.value.push(0)
  }
}
function deleteTimer(id){
  ids.value.splice(ids.value.findIndex(item=>item==id),1)
}

</script>

<style lang="scss" scoped>

</style>