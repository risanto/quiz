<template>
  <div class="result">
    <div class="title">{{ result.title }}</div>
    <div class="desc">{{ result.desc }}</div>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: ["results", "totalCorrect"],
  computed: {
    result() {
      for (let i = 0; i < this.results.length; i++) {
        let res = this.results[i];

        if (res.min <= this.totalCorrect && res.max >= this.totalCorrect) {
          return res;
        }
      }
    },
  },
};
</script>
