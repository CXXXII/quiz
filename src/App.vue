<template>
  <div class="ctr">
    <countdown :seconds="seconds" :showCounter="showCounter"/>
    <transition-group name="fade">
      <questions
          v-if="(questionsAnswered < questions.length)"
          :questions="questions"
          :questionsAnswered="questionsAnswered"
          @question-answered="questionsAnsweredFunc"
      />
      <result v-else
              :totalCorrect="totalCorrect"
              :results="results"
      />
    </transition-group>
    <button
        type="button"
        class="reset-btn"
        @click.prevent="reset"
        v-if="(questionsAnswered === questions.length)"
    >Reset
    </button>
  </div>
</template>

<script>
import Questions from "@/components/Questions.vue";
import Result from "@/components/Result.vue";
import Countdown from "@/components/Countdown.vue"

export default {
  name: "App",
  components: {Questions, Result, Countdown},
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      seconds: 30,
      showCounter: true,
      questions: [
        {
          q: 'What does the setInterval method return in the browser?',
          e: 'setInterval(() => console.log("Hi"), 1000)',
          answers: [
            {
              text: 'unique id',
              is_correct: true
            },
            {
              text: 'a given number of milliseconds',
              is_correct: false
            },
            {
              text: 'passed function',
              is_correct: false
            },
            {
              text: 'undefined',
              is_correct: false
            }
          ]
        },
        {
          q: 'What will be the result?',
          e: '!!null; !!""; !!1;',
          answers: [
            {
              text: 'false true false',
              is_correct: false
            },
            {
              text: 'false false true',
              is_correct: true
            },
            {
              text: 'false true true',
              is_correct: false
            },
            {
              text: 'true true false',
              is_correct: false
            }
          ]
        },
        {
          q: 'What will be the output?',
          e: 'console.log(🥑💻)',
          answers: [
            {
              text: '"🥑💻"',
              is_correct: true
            },
            {
              text: '257548',
              is_correct: false
            },
            {
              text: 'A line containing code symbols',
              is_correct: false
            },
            {
              text: 'Error',
              is_correct: false
            }
          ]
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Answers with explanation here https://t.me/frontend_tests"
        },
        {
          min: 3,
          max: 3,
          title: "Congratulations!",
          desc: "The questions were taken from here https://t.me/frontend_tests"
        }
      ]
    }
  },
  methods: {
    questionsAnsweredFunc(is_correct) {
      is_correct ? this.totalCorrect++ : "";
      this.questionsAnswered++;
      this.questionsAnswered !== this.questions.length ? this.seconds = 30 : "";
    },
    reset() {
      this.totalCorrect = 0;
      this.questionsAnswered = 0;
      this.seconds = 30;
      this.showCounter = true;
      this.startCount()
    },
    startCount() {
      const counter = setInterval(() => {
        if ((this.seconds > 0) && (this.questionsAnswered !== this.questions.length)) {
          this.seconds--
        } else if (this.questionsAnswered === this.questions.length) {
          this.showCounter = false;
          clear()
        } else {
          this.questionsAnswered++;
          this.seconds = 30;
        }
      }, 1000);
      function clear() {
        clearInterval(counter);
      }

    },
  },
  mounted() {
    this.startCount();
  }
}
</script>

<style>

</style>
