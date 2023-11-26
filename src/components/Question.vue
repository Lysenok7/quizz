<template>
  <div :class="`question ${additionalClasses}`">
    <h3 class="question__title">{{question.label}}</h3>
    <ul class="question__answers">
      <li v-for="(answer, index) in question.answers" @click="$emit('onAnswerClick', index)" class="question__answer" >
        {{answer}}
      </li>
    </ul>
  </div>
</template>

<script setup>
const props = defineProps(['question', 'additionalClasses'])

</script>

<style>
  .question__title{
    font-size: 18px;
    font-weight: 500;
    text-align: center;
    color: #fff;
    margin-bottom: 24px;
  }
  .question{
    position: absolute;
    opacity: 0;
    visibility: hidden;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    transition: .3s all ease-in-out;
  }
  .question.active{
    opacity: 1;
    visibility: visible;
  }
  .question__answers{
    display: grid;
    gap: 24px;
    max-width: 500px;
    margin: auto;
    grid-template-columns: repeat(2, 1fr);
  }
  .question__answer{
    height: 100px;
    width: 100%;
    border: 2px solid #9f989a;
    border-radius: 8px;
    line-height: 100px;
    text-align: center;
    font-size: 18px;
    transition: .3s all ease-in-out;
    cursor: pointer;
  }
  .question__answer:hover{
    color: #fff;
    border: 2px solid #fff;
  }
</style>