<script setup>
import {onMounted, ref} from "vue";
import Question from "../components/Question.vue";
import Results from "../components/Results.vue";
const isLoading = ref(false);
  const questions = ref([])
  const activeIndex = ref(0)
  let correctAnswersCount = ref(0);
  const fetchQuestions = async () => {
     isLoading.value = true;
     const questionsJson = await fetch('/questions.json')
     questions.value = await questionsJson.json();
     console.log(questions.value)
     isLoading.value = false;
  }
  const changeQuestionToNext = (questionIndex, answerIndex) => {
    activeIndex.value += 1;
    if (questions.value[questionIndex].correct === answerIndex){
      correctAnswersCount.value++;
    }
  }
  onMounted(() => {
    fetchQuestions()
  })
</script>

<template>
  <main>
    <div v-if="isLoading">Loading...</div>
    <div v-else>
      <div v-if="activeIndex === questions.length">
        <Results :correctAnswers="correctAnswersCount" :totalQuestions="questions.length"/>
      </div>
      <div v-else v-for="(question, index) in questions">
        <Question @onAnswerClick="(answerIndex)=>changeQuestionToNext(index, answerIndex)" :question="question" :additionalClasses="activeIndex === index ? 'active' : ''"/>
      </div>
    </div>
  </main>
</template>
