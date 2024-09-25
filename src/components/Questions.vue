<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        v-bind:style="{
          width: `${(questionsAnswered / questions.length) * 100}%`,
        }"
      ></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade" v-bind:css="true">
      <div
        class="single-question"
        v-for="(question, qi) in questions"
        v-bind:key="question.q"
        v-show="qi === questionsAnswered"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            v-bind:key="answer.text"
            v-on:click.prevent="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ["questions", "questionsAnswered"],
  emits: ["question-answered"],
  methods: {
    selectAnswer(is_correct) {
      this.$emit("question-answered", is_correct);
    },
  },
};
</script>
