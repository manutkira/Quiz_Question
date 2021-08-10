<template>
  <div class="ctr">
    <transition name="fade">
      <question
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />

      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>

    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import "./main.css";
import question from "./src/components/question.vue";
import Result from "./src/components/result.vue";
export default {
  components: { question, Result },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "Find the missing letter: C_ke",
          answers: [
            {
              text: "e",
              is_correct: false,
            },
            {
              text: "a",
              is_correct: true,
            },
            {
              text: "i",
              is_correct: false,
            },
          ],
        },
        {
          q: "Who is the richest?",
          answers: [
            {
              text: "Jeff Bezos",
              is_correct: true,
            },
            {
              text: "Jack Ma",
              is_correct: false,
            },
            {
              text: "Steve Jobs",
              is_correct: false,
            },
            {
              text: "Steve Harvey",
              is_correct: false,
            },
          ],
        },
        {
          q: "how hot is the surface of the sun?",
          answers: [
            {
              text: "15000000Degrees",
              is_correct: false,
            },
            {
              text: "20000000Degrees",
              is_correct: false,
            },
            {
              text: "10000000Degrees",
              is_correct: true,
            },
            {
              text: "25000000Degrees",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }
      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>
