<script setup>
import Question from "../components/Question.vue"
import QuestionHeader from "../components/QuizHeader.vue"
import {useRoute} from "vue-router";
import {ref, watch, computed} from "vue";
import quizes from "../data/quizes.json"

const route = useRoute()
const quizId = parseInt(route.params.id)
const currentQuestionIndex = ref(0)
const quiz = quizes.find(q => q.id === quizId)


const questionStatus = computed(() => `${currentQuestionIndex.value}/${quiz.questions.length}`)
const barPercentage = computed(() => `${currentQuestionIndex.value/quiz.questions.length * 100}%`)
</script>

<template>
  <div>
    <QuestionHeader
        :questionStatus="questionStatus"
        :barPercentage="barPercentage"
    />
    <div>
      <Question :question="quiz.questions[currentQuestionIndex]"/>
    </div>
  </div>
</template>