<template>
  <div class="about">
    <h1>This is an about page</h1>
    <h6 v-html="rawHtml"></h6>
    <p>Using text interpolation: {{ rawHtml }}</p>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      rawHtml:
        '<h1>This is to see how v-html works</h1> <span style="color: green">This should be green.</span>',
    }
  },
}
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    /* display: flex; */
    align-items: center;
  }
}
</style>
