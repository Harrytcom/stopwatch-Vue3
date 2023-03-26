<template>
  <div class="stopwatches-container">
    <h1>Stopwatches</h1>
    <div class="stopwatches">
      <Stopwatch v-for="(stopwatch, index) in stopwatches" :key="index" :index="index" @remove="removeStopwatch" />
    </div>
    <button @click="addStopwatch">Add Stpwtch</button>
  </div>
</template>

<script>
import Stopwatch from './Stopwatch.vue'

export default {
  components: {
    Stopwatch
  },
  data() {
    return {
      stopwatches: []
    }
  },
  methods: {
    addStopwatch(stopwatch) {
      this.stopwatches.push(stopwatch)
    },
    removeStopwatch(stopwatch) {
      this.stopwatches = this.stopwatches.filter(el => el.id !== stopwatch.id)
    }
  }
}
</script>