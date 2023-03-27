<template>
  <div class="stopwatch-container">
      <Stopwatch v-for="index in stopwatches" :key="index" :index="index" />
        <add-stopwatch @click="addStopwatch" />
  </div>
</template>

<script>
import Stopwatch from './Stopwatch.vue'
import addStopwatch from './addStopwatch.vue'

export default {
  components: {
    Stopwatch,
    addStopwatch
  },
  data() {
    return {
      stopwatches: []
    }
  },
  methods: {
    addStopwatch() {
      this.stopwatches.push({})
    },
  }
}
</script>

<style>
  .stopwatch-container {
    font-family: 'Gotham Pro', sans-serif, monospace;
    font-weight: 400;
    font-size: 22px;
    line-height: 21px;
    display: grid;
    grid-template-columns: 220px;
    grid-template-rows: auto;
    gap: 50px;
    justify-content: center;
    padding: 70px 0 80px;
    background-color: var(--primary-bg-color);
  }

  @media (min-width: 767.98px) {
    .stopwatch-container {
      grid-template-columns: repeat(2, 220px);
    }
  }

  @media (min-width: 1023.98px) {
    .stopwatch-container {
      grid-template-columns: repeat(3, 220px);
    }
  }
  </style>