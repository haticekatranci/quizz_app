<script setup>
import { ref, computed } from 'vue'

const questions = ref([
  {
    question: 'What is Vue JS?',
    answer:0,
    options: [
       'A front-end framework',
       'A library',
       'An ice cream maker',

    ]
  },
  {
    question: 'What is Vuex?',
    answer:2,
    options: [
       'Vue with an x',
       'A cheese selection',
       'State manangement library',

    ]
  },
  {
    question: 'What is Vue Router used for?',
    answer:1,
    options: [
       'Walking in space',
       'A routing library for VUe JS',
       'Burger suauce',
       'Quizzes',
    ]
  }
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
const score = computed(() => {
  let value = 0 
  questions.value.map(q => {
    if (q.selected == q.answer) {
      value++
    }
  })
  return value 
})

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question 
})

const SetAnswer = evt => {
  questions.value[currentQuestion.value].selected = evt.target.value
  evt.target.value = null
}

const NextQuestion = () => {
  if(currentQuestion.value < questions.value.length -1) {
    currentQuestion.value++
  }else {
    quizCompleted.value = true
  }
}

</script>

<template>
 <main class="app">
  <h1> The quiz</h1>
  <section class="quiz">
    <div class="quiz-info">
      <span class="question">{{ getCurrentQuestion.question }}</span>
      <span class="score">Score {{ score }} / {{ questions.length }}</span>
    </div>
  </section>
 </main>
</template>

<style >
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Monstserrat', sans-serif;
}
body {
  background-color: #271C36;
  color: #fff;
}

</style>
