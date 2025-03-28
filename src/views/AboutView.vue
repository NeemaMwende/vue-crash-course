<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p>Hello, {{ name }}!</p>
    <h6 v-html="rawHtml"></h6>
    <p>Using text interpolation: {{ rawHtml }}</p>
    <div :id="'user-' + userId">User Profile</div>
    <button :class="{ active: isActive }">Click Me</button>
    <p>{{ number + 1 }}</p>
    <time :title="toTitleDate(date)" :datetime="date">
      {{ formatDate(date) }}
    </time>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      rawHtml:
        '<h1>This is to see how v-html works <span style="color: green">This should be green.</span> </h1> ',
      name: 'Neema ',
      userId: 123,
      isActive: true,
      number: 5,
      date: new Date().toISOString(),
    }
  },
  methods: {
    toTitleDate(date: string | number | Date) {
      return new Date(date).toLocaleString('en-US', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit',
      })
    },
    formatDate(date: string | number | Date) {
      return new Date(date).toLocaleDateString('en-US', {
        year: 'numeric',
        month: 'short',
        day: 'numeric',
      })
    },
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
