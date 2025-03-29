<template>
  <div class="about">
    <p v-if="isLoggedIn">Welcome, user!</p>
    <p v-else>Please log in.</p>
    <p v-show="isVisible">I am visible</p>

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

    <ul>
      <li v-for="(item, index) in items" :key="index">{{ index + 1 }}. {{ item }}</li>
    </ul>

    <!-- v-on for onclick, mouseover, input -->
    <button v-on:click="sayHello">Click me</button>
    <button @click="sayHello">Shorter way</button>

    <!-- v-model – Two-Way Binding -->
    <input v-model="yourname" placeholder="Enter your name" />
    <p>Hello, {{ yourname }}</p>

    <!-- v-pre – Skips Compilation
     Vue ignores the element’s content. -->
    <p v-pre>{{ This will not be compiled }}</p>

    <!-- v-text: sets textContent of element -->
    <p v-text="message"></p>

    <!-- Event-Specific Directives -->
    <button @click.stop="stopPropagation">Click Me (Stop Event)</button>

    <form @submit.prevent="submitForm">
      <input type="text" v-model="formData" placeholder="Type something..." />
      <button type="submit">Submit</button>
    </form>

    <!-- v-on:keyup.enter -->
    <input v-model="message" @keyup.enter="sendMessage" placeholder="Press Enter" />

    <!-- v-slot Example (Scoped Slots) -->
    <ReusableComponent>
      <template v-slot:header>
        <h2>Custom Header</h2>
      </template>
    </ReusableComponent>

    <!-- v-memo: Optimizing performance -->
    <p v-memo="[count]">Count: {{ count }}</p>
    <button @click="increment">Increment</button>

    <h2>Counter: {{ count }}</h2>
    <button @click="increment">Increment</button>

    <!-- This paragraph will NOT re-render unless count changes -->
    <p v-memo="[count]">This will only update when count changes: {{ count }}</p>

    <!-- This always re-renders -->
    <p>Current Time: {{ new Date().toLocaleTimeString() }}</p>
    <p v-memo="[count]">Current Time: {{ time }}</p>
  </div>
</template>

<script lang="ts">
import ReusableComponent from '../views/ReusableComponent.vue'

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
      isLoggedIn: true,
      isVisible: true,
      items: ['Vue', 'React', 'Angular'],
      yourname: '',
      message: 'Hello Vue!',
      formData: '',
      count: 0,
      time: new Date().toLocaleTimeString(),
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
    sayHello() {
      alert('Hello from Vue!')
    },
    stopPropagation() {
      alert('Event propagation stopped!')
    },
    submitForm() {
      alert(`Form submitted with: ${this.formData}`)
      this.formData = ''
    },
    sendMessage() {
      alert(`You pressed Enter: ${this.message}`)
    },
    increment() {
      this.count++
    },
  },
  components: {
    ReusableComponent,
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
