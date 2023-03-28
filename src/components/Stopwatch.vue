<template>
    <div class="stopwatch">
        <div class="stopwatch__time" :class="{active: isTimerActive}">{{ getTime }}</div>
        <div class="stopwatch__btns" :class="{active: isTimerActive}">
            <button class="start" @click="startTimer" v-show="!isTimerActive">
                <img src="@/assets/images/triangle.png" alt="">
            </button>
            <button class="pause" @click="pauseTimer" v-show="isTimerActive">
                <img src="@/assets/images/pause.png" alt="">
            </button>
            <button class="stop" @click="stopTimer">
                <img src="@/assets/images/square.png" alt="">
            </button>
            <button class="stopwatch__btns-delete" @click="$emit('deleteTimer', props.id)">х</button>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
const time = ref(0)
const isTimerActive = ref(false)
let mySetTimeout;

const props = defineProps(['id'])

const getTime = computed(()=>{
    if(time.value>=60){
        if(time.value<3600){
            let minut = Math.floor(time.value/60);
            let sec = time.value%60;
            return `${minut}:${sec}`;
        }else{
            let hour = Math.floor(time.value/3600);
            let minut = Math.floor(Math.floor(time.value/60)%60)
            let sec = time.value%60;
            return `${hour}:${minut}:${sec}`
        }
    }else{
        return time.value
    }
})


function startTimer(){
    
    isTimerActive.value=true

    mySetTimeout=setTimeout(()=>{
        time.value+=1;
        startTimer()
    }, 1000)
    
}

function pauseTimer(){
    isTimerActive.value=false
    clearTimeout(mySetTimeout)

}
function stopTimer(){
    time.value=0;
    isTimerActive.value=false
    clearTimeout(mySetTimeout)
}

</script>

<style lang="scss" scoped>

</style>