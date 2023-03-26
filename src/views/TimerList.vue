<template>
  <section class="timer">
    <div class="container">
      <div class="timer__body">
        <ul class="timer__list">
          <timer-item 
            v-for="item in timerList" 
            :key="item.id" 
            :item="item" 
          />
          <li class="timer__column">
            <button type="button" 
              class="timer__btn-add btn" 
              @click="addTimer">
            </button>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";
import TimerItem from "@/components/TimerItem.vue";
const timerList = ref([
  {
    id: 1,
    time: "0",
  },
  {
    id: 2,
    time: "0",
  },
  {
    id: 3,
    time: "0",
  },
]);

const addTimer =()=> {
  timerList.value.push(
    {
       id: timerList.value.length + 1, 
       time: "0",
  })
}
</script>

<style lang="scss">
@import "@/assets/scss/variables.scss";
.timer {
  padding-top: 30px;

  .timer__list {
    display: flex;
    flex-wrap: wrap;
    column-gap: 50px;
    row-gap: 45px;
  }

  .timer__column {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 225px;
    height: 120px;

    .timer__btn-add {
      display: flex;
      width: 100%;
      height: 120px;
      background-color: #696969;
      transform: background-color 0.5s ease-in;

      &:hover::before,
      &:hover::after ,
      &:focus::before,
      &:focus::after {
        outline: none;
        background-color: $color-white;
      }

      &::before,
      &::after {
        position: absolute;
        content: '';
        width: 3px;
        height: 20px;
        background-color: $color-gray;
      }

      &::before {
        top: calc(50% - 10px);
        left: calc(50% - 1.5px);
      }
      &::after {
        top: calc(50% - 10px);
        left: calc(50% - 1.5px);
        transform: rotate(90deg);
      }
    }
  }

  @media (max-width: $sm-width) {
    .timer__list {
      justify-content: center;
      align-items: center;
    }
  }
}
</style>