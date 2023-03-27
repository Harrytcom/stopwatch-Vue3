<template>
    <div class="stopwatch">
      <div :class="{ 'stopwatch__timer': true, 'is-active': running }">
        <div v-if="time < 60000">{{ formatSeconds }}</div>
        <div v-else-if="time < 3600000">{{ formatMinutes }}</div>
        <div v-else>{{ formatHours }}</div>
      </div>
      <span :class="{ 'stopwatch__bar': true, 'white-bg': running }"></span>
      <div class="stopwatch__controls">
        <button class="stopwatch__start" @click="start" v-if="!running || paused" :disabled="running">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M0 20V0L17 10L0 20Z" :fill="running ? '#fff' : '#9e9e9e'" />
          </svg>
        </button>
        <button class="stopwatch__pause" @click="pause" v-show="running && !paused">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="7" width="3" height="20" :fill="running ? '#fff' : '#9e9e9e'" />
            <rect width="3" height="20" :fill="running ? '#fff' : '#9e9e9e'" />
          </svg>
        </button>
        <button class="stopwatch__stop" @click="stop">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect width="20" height="20" :fill="running ? '#ffffff' : '#9e9e9e'" />
          </svg>
        </button>
      </div>
    </div>
</template>

<script>
export default {
  props: {
    index: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      running: false,
      paused: false,
      time: 0,
      timer: null,
    };
  },
  methods: {
    start() {
      this.running = true;
      this.paused = false;
      this.timer = setInterval(() => {
        this.time += 10;
      }, 10);
    },
    pause() {
      this.running = false;
      this.paused = true;
      clearInterval(this.timer);
    },
    stop() {
      this.running = false;
      this.paused = false;
      clearInterval(this.timer);
      this.time = 0;
    },
  },
  computed: {
    formatSeconds() {
      let seconds = Math.floor(this.time / 1000);
      return seconds.toString().padStart(2, "0");
    },
    formatMinutes() {
      let minutes = Math.floor(this.time / 60000);
      let seconds = Math.floor((this.time % 60000) / 1000);
      return `${minutes.toString().padStart(2, "0")}:${seconds.toString().padStart(2, "0")}`;
    },
    formatHours() {
      let hours = Math.floor(this.time / 3600000);
      let minutes = Math.floor((this.time % 3600000) / 60000);
      let seconds = Math.floor((this.time % 60000) / 1000);
      return `${hours.toString().padStart(2, "0")}:${minutes.toString().padStart(2, "0")}:${seconds.toString().padStart(2, "0")}`;
    },
  },
};
</script>

<style>
  @font-face {
    font-family: 'Gotham Pro';
    font-weight: 400;
    font-style: normal;
    src: url(./fonts/GothamPro.woff2) format('woff2'),
         url(./fonts/GothamPro.woff) format('woff'),
         url(./fonts/GothamPro.ttf) format('truetype');
  }

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :root {
    --primary-bg-color: #353638;
    --secondary-bg-color: #696969;
    --primary-color: #9e9e9e;
    --accent-color: #fff;
  }

  .stopwatch {
    background-color: var(--secondary-bg-color);
    color: var(--primary-color);
    height: 120px;
    display: flex;
    flex-flow: column nowrap;
    justify-content: space-evenly;
    align-items: center;
  }

  .stopwatch__bar {
    height: 1px;
    width: 100%;
    background-color: var(--primary-color);
  }

  .stopwatch__timer {
    font-feature-settings: "tnum";
    font-variant-numeric: tabular-nums;
  }

  .stopwatch__controls {
    display: flex;
    gap: 50px;
  }

  .is-active {
    color: var(--accent-color);
  }

  .white-bg {
    background-color: var(--accent-color);
  }

  .stopwatch__controls button {
    background: none;
    border: none;
    color: inherit;
    cursor: pointer;
    font-family: inherit;
    font-size: medium;
    font-weight: inherit;
    line-height: normal;
    padding: 0;
    text-align: center;
    text-decoration: none;
    text-transform: none;
  }

  .add-btn {
    background-color: var(--secondary-bg-color);
    height: 120px;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: center;
  }
</style>
