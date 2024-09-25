<template>
  <GithubForkRibbonVue
    v-bind:title="forkRibbon.title"
    v-bind:url="forkRibbon.url"
    v-bind:color="forkRibbon.color"
  />

  <div class="ctr">
    <transition name="fade" mode="out-in" v-bind:css="true">
      <questions-vue
        v-if="questionsAnswered < questions.length"
        v-bind:questions="questions"
        v-bind:questionsAnswered="questionsAnswered"
        v-on:question-answered="questionAnswered"
      />
      <result-vue
        v-else
        v-bind:results="results"
        v-bind:totalCorrect="totalCorrect"
      />
    </transition>

    <button
      type="button"
      class="reset-btn"
      v-on:click.prevent="reset"
      v-if="this.questionsAnswered === this.questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import GithubForkRibbonVue from "./components/GithubForkRibbon.vue";
import QuestionsVue from "./components/Questions.vue";
import ResultVue from "./components/Result.vue";

export default {
  name: "App",
  components: {
    QuestionsVue,
    ResultVue,
    GithubForkRibbonVue,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "What is 2 + 2?",
          answers: [
            {
              text: "4",
              is_correct: true,
            },
            {
              text: "3",
              is_correct: false,
            },
            {
              text: "Fish",
              is_correct: false,
            },
            {
              text: "5",
              is_correct: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: "5",
              is_correct: false,
            },
            {
              text: "7",
              is_correct: false,
            },
            {
              text: "6",
              is_correct: true,
            },
            {
              text: "12",
              is_correct: false,
            },
          ],
        },
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
      forkRibbon: {
        title: "Fork me on GitHub",
        url: "https://github.com/Rizwan-Hasan/Quiz-App-Vue",
        color: "#35495e",
      },
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect += 1;
      }
      this.questionsAnswered += 1;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>
