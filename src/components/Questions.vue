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
