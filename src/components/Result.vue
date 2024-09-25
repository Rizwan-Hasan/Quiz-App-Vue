<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">{{ results[resultIndex].desc }}</div>
  </div>
</template>

<script>
export default {
  props: ["results", "totalCorrect"],
  computed: {
    resultIndex() {
      let index = 0;

      this.results.forEach((element, elmement_index) => {
        if (
          element.min <= this.totalCorrect &&
          element.max >= this.totalCorrect
        ) {
          index = elmement_index;
        }
      });

      return index;
    },
  },
};
</script>
