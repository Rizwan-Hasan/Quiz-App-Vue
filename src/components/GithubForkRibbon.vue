<template>
  <a
    class="github-fork-ribbon"
    v-bind:href="url"
    v-bind:data-ribbon="title"
    v-bind:title="title"
    v-bind:style="{ '--bgColor': color }"
  >
    {{ title }}
  </a>
</template>

<script>
export default {
  props: ["title", "url", "color"],
};
</script>

<style scoped lang="scss">
@import url("https://cdnjs.cloudflare.com/ajax/libs/github-fork-ribbon-css/0.2.3/gh-fork-ribbon.min.css");

.github-fork-ribbon:before {
  background-color: var(--bgColor);
}
</style>
