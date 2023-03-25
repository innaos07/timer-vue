<template>
  <li class="timer__item item-timer">
    <div class="item-timer__top">
      <span class="item-timer__time"> {{ item.time }}</span>
    </div>

    <div class="item-timer__btns">
  
      <button
      v-if="isRunning"
      type="button"
        class="item-timer__btn item-timer__btn-pause"
        :class="{'item-timer__btn-start-pause--active' : isRunning}"
        @click="stop"
      > </button>
      <button 
       v-else
        type="button"
        class="item-timer__btn item-timer__btn-start"
        :class="{'item-timer__btn-start--active' : isRunning}"
        @click="start"
      ></button>
      <button
        type="button"
        class="item-timer__btn item-timer__btn-reset"
        :class="{'item-timer__btn-reset--active' : isRunning}"
        @click="reset"
      ></button>
    </div>
  </li>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  item: {
    type: Object,
    default: () => {},
  },
});

const isRunning = ref(false);
// const isStop = ref(false);
const timeActive = ref(null);
const timeStart = ref(null);
const timeStop = ref(0);
const timerStopped = ref(null);



const start = () => {
  if(isRunning) {
    false
  }
  timeStart.value = timeStart.value === null ?  new Date() : timeStart.value;

  if(timerStopped.value !== null ) {
     timeStop.value += (new Date() - timerStopped.value) 
  }

  timeActive.value = setInterval(timerRunning, 100);
  isRunning.value = true;
};

const stop = () => {
  isRunning.value = false;
  clearInterval(timeActive.value);
  timerStopped.value = new Date();
};

const reset =()=> {
  isRunning.value = false;
  clearInterval(timeActive.value);
  props.item.time = "0";
  timeStart.value = null;
  timerStopped.value = null;
  timeStop.value = 0;
}

const timerRunning = () => {
  const currentDate = new Date();
  const diffTime = new Date(currentDate - timeStart.value - timeStop.value);
  setTimer(diffTime)
};

const setTimer =(time)=> {
  const hour = time.getUTCHours() < 10 ? "0" + time.getUTCHours(): time.getUTCHours();
  const min = time.getMinutes() < 10 ? "0" + time.getMinutes() : time.getMinutes();
  const sec = time.getUTCSeconds() < 10 ? "0" + time.getUTCSeconds() : time.getUTCSeconds();

  sec >= 1 && min == 0 && hour == 0 ? props.item.time = sec :
  sec >= 1 && min >= 1 && hour == 0 ? props.item.time = `${min}:${sec}`:
  sec >= 1 && min >= 1 && hour >= 1 ? props.item.time = `${hour}:${min}:${sec}` : "0"
}
</script>

<style lang="scss">
@import "@/assets/scss/variables.scss";
.item-timer {
  position: relative;
  // flex: 1 1 33.333%;
  display: flex;
  flex-direction: column;
  width: 225px;
  min-height: 120px;
  background-color: #696969;

  .item-timer__top,
  .item-timer__btns {
    display: flex;
    align-items: center;
    min-height: 60px;
  }

  .item-timer__top {
    justify-content: center;
    padding-top: 22px;
    padding-bottom: 20px;
    border-bottom: 1px solid $color-gray;
  }

  .item-timer__time {
    text-align: center;
    font-weight: 400;
    font-size: 22px;
    line-height: 21px;
    text-align: center;

    color: #ffffff;
  }

  .item-timer__btns {
    justify-content: space-between;
    padding: 20px 70px;
    border-top: 1px solid $color-gray;
  }

  .item-timer__btn {
    padding: 0;
    position: relative;
    display: flex;
    border: none;
    border-radius: 0;
    outline: none;
    background-color: transparent;
    cursor: pointer;
  }

  .item-timer__btn-start {
    width: 17px;
    height: 20px;

    border-width: 10px;
    border-style: solid;
    border-color: transparent;
    border-left: 17px solid $color-gray;
    transition: border-left 0.5s ease-in;

    &--active {
      border-left: 17px solid $color-white;
    }
 
  }

  .item-timer__btn-pause {
    position: relative;
    width: 10px;
    height: 20px;
    &--active::before,
    &--active::after {
      background-color: $color-white;
    }

    &::before,
    &::after {
      position: absolute;
      content: '';
      top: 0;
      width: 3px;
      height: 20px;
      background-color: $color-gray;

      // &--active {
      // background-color: $color-white;
      // }
    }

    &::before {
      left: 0;
    }

    &::after {
      right: 0;
    }

   
    
  }

  .item-timer__btn-reset {
    width: 20px;
    height: 20px;
    background-color: $color-gray;
    transition: background-color 0.5s ease-in;

    &--active {
      background-color: $color-white;
    }
  }
}
</style>