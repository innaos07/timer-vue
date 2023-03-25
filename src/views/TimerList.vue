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
        time: '0'
    },
    {
        id: 2,
        time: '0'
    },
    {
        id: 3,
        time: '0'
    }
])

</script>

<style lang="scss">
@import "@/assets/scss/variables.scss";
.timer {
    position: fixed;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;

    .timer__body {

    }

    .timer__list {
        display: flex;
        flex-wrap: wrap;
        column-gap: 50px;
        row-gap: 45px;
    }
}

</style>