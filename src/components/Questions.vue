<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>

    <TransitionGroup
      mode="out-in"
      enterActiveClass="animate__animated animate__bounce"
      leaveActiveClass="animate__animated animate__backOutDown"
    >
      <div
        class="single-question"
        v-for="(question, qIdx) in questions"
        :key="question.q"
        v-show="questionsAnswered === qIdx"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            :key="answer"
            @click.prevent="handleAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  name: "Questions",
  props: ["questions", "questionsAnswered"],
  emits: ["handleAnswer"],
  methods: {
    handleAnswer(isCorrect) {
      this.$emit("handleAnswer", isCorrect);
    },
  },
};
</script>

<style>
.animate__backOutDown {
  position: absolute;
}
</style>
