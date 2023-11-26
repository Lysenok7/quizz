<template>
  <ul class="stats">
    <li class="stat">
      <div class="stat__content">
        {{correctAnswers}}/{{totalQuestions}}
        <span class="stat__description">Correct Answers</span>
      </div>
    </li>
    <li class="stat">
      <div class="stat__content">
        {{wrongAnswers}}/{{totalQuestions}}
        <span class="stat__description">Wrong answers</span>
      </div>
    </li>
    <li class="stat">
      <div class="stat__content">
        {{correctPercentage}}%
        <span class="stat__description">Correct Answers in percents</span>
      </div>

    </li>
    <li class="stat">
      <div class="stat__content">
        {{wrongPercentage}}%
        <span class="stat__description">Wrong answers in percents</span>
      </div>

    </li>
  </ul>
</template>

<script setup>
import {computed} from "vue";

const props = defineProps(['correctAnswers', 'totalQuestions'])
const wrongAnswers = computed(() => {
  return props.totalQuestions - props.correctAnswers;
})
const correctPercentage = computed(() => {
  return 100 / props.totalQuestions * props.correctAnswers
})
const wrongPercentage = computed(() => {
  return 100 - correctPercentage.value
})
</script>

<style scoped>
.stats{
  display: grid;
  gap: 24px;
  width: 550px;
  margin: auto;
  grid-template-columns: repeat(2, 1fr);
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.stat{
  height: 100px;
  width: 100%;
  border: 2px solid #fff;
  color: #fff;
  line-height: 100px;
  border-radius: 8px;
  text-align: center;
  font-size: 18px;
  transition: .3s all ease-in-out;
  cursor: pointer;
}
.stat__description{
  font-size: 14px;
  color: #9f989a;
}
.stat__content{
  display: inline-block;
  line-height: normal;
  font-size: 18px;
}
</style>