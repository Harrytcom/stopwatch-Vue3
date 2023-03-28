<template>
  <div class="stopwatch-container">
    <stopwatch v-for="item in stopwatches" :key="item.id" />
    <add-btn @add="addBtn" />
  </div>
</template>

<script>
import Stopwatch from './Stopwatch.vue'
import addBtn from './addBtn.vue'

export default {
  components: {
    Stopwatch,
    addBtn
  },
  data() {
    return {
      stopwatches: [
        { id: 1 }
      ]
    }
  },
  methods: {
    addBtn() {
      this.stopwatches.push({
        id: this.stopwatches.length + 1
      })
    },
  }
}
</script>

<style>
.stopwatch-container {
  font-family: 'Gotham Pro', sans-serif, monospace;
  font-weight: 400;
  font-size: 1.375rem;
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