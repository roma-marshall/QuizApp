<template>
  <main class="flex h-screen justify-center">
    <CompleteOverlay
        v-if="quizDone"
    />
    <div class="bg-white container mx-auto shadow-lg rounded-lg px-12 py-6">
      <div class="text-right text-gray-800">
        <p class="text-sm leading-3">Score</p>
        <p class="font-bold">{{ score }}</p>
      </div>
      <div class="bg-white shadow-lg p-2 rounded-full w-full h-10">
        <div
            class="bg-blue-700 rounded-full h-full"
            :style="`width: ${timer}%`"
        >
        </div>
      </div>
      <div class="rounded-lg bg-gray-100 p-2 morph-1 text-center font-bold text-gray-800 mt-8">
        <div class="bg-white p-5">
          {{ currentQuestion.question }}
        </div>
      </div>
      <div class="mt-8">
        <div
            v-for="(choice, item) in currentQuestion.choices"
            :key="item"
        >
          <div
              class="morph-1 bg-gray-100 p-2 rounded-lg mb-3 relative"
              :ref="optionChosen"
              @click="onOptionClicked(choice, item)"
          >
            <!--            <div class="bg-blue-700 p-1 transform rotate-45 rounded-md text-white h-10 w-10-->
            <!--                fond-bold absolute right-0 top-0 shadow-md">-->
            <!--              <p class="transform -rotate-45">+10</p>-->
            <!--            </div>-->
            <div class="bg-white rounded-lg font-bold flex p-2">
              <div class="bg-gray-500 px-4 py-2 rounded-lg text-white">{{ item }}</div>
              <div class="flex items-center pl-6">{{ choice }}</div>
            </div>
          </div>
        </div>
        <div class="mt-8 text-center">
          <div class="h-1 w-12 bg-gray-800 rounded-full mx-auto"></div>
          <p class="text-gray-800 font-bold">{{ page }} / {{ question.length }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import {ref, onMounted} from 'vue';
import CompleteOverlay from './CompleteOverlay.vue';

export default {
  setup() {
    let timer = ref(100)
    let approveClick = true
    let itemsRef = []
    let score = ref(0)
    let page = ref(1)
    let quizDone = ref(false)
    let questionCounter = ref(0)
    const currentQuestion = ref({
      question: '',
      answer: 1,
      choices: []
    })
    const question = [
      {
        question: '2 + 2',
        answer: 0,
        choices: ['4', '-1', '0', '10']
      },
      {
        question: '10 - 5',
        answer: 1,
        choices: ['-4', '5', '33', '-5']
      },
      {
        question: '3 * 2',
        answer: 2,
        choices: ['-4', '0', '6', '41']
      },
      {
        question: '55 / 5',
        answer: 3,
        choices: ['3', '-16', '30', '11']
      },
    ]
    const loadQuestion = () => {
      approveClick = true
      questionCounter.value++
      if (question.length > questionCounter.value)
        currentQuestion.value = question[questionCounter.value]
      else {
        quizDone.value = true
        timer.value = 100
      }
      if (question.length !== page.value)
        page.value++
    }
    const countDownTimer = () => {
      let interval = setInterval(() => {
        if (timer.value > 0 && quizDone.value === false)
          timer.value--
        else
          clearInterval(interval)
      }, 100)
    }
    const onQuizStart = () => {
      currentQuestion.value = question[questionCounter.value]
    }
    const optionChosen = (el) => {
      if (el)
        itemsRef.push(el)
    }
    const clearSelected = (divContainer) => {
      setTimeout(() => {
        divContainer.classList.remove('bg-green-400')
        divContainer.classList.remove('bg-red-400')
        loadQuestion()
      }, 1000)
    }
    const onOptionClicked = (choice, item) => {
      if (approveClick) {
        const divContainer = itemsRef[item]
        const optionID = item++
        if (currentQuestion.value.answer === optionID) {
          score.value = score.value + 10
          divContainer.classList.add('bg-green-400')
          if (timer.value + 10 <= 100)
            timer.value += 10
          else
            timer.value = 100
        } else {
          divContainer.classList.add('bg-red-400')
        }
        clearSelected(divContainer)
        approveClick = false
      }
    }
    onMounted(() => {
      onQuizStart()
      countDownTimer()
    })
    return {
      currentQuestion,
      question,
      questionCounter,
      onQuizStart,
      onOptionClicked,
      optionChosen,
      score,
      page,
      timer,
      quizDone
    }
  },
  components: {
    CompleteOverlay
  }
}
</script>

<style scoped>
.morph-1 {
  box-shadow: 6px 6px 18px rgba(0, 0, 0, 0.09), -6px -6px 18px #ffffff;
}
</style>