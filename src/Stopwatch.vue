<template>
  <div class="container">
    <div class="stopwatch-container">
      <div class="stopwatch">
        <p :class="{stopwatch__timer: true, 'is-active': running}">
          {{ formatTime }}
        </p>
        <span :class="{'stopwatch__bar': true, 'white-bg': running}"></span>
        <div class="stopwatch__controls">
          <button class="stopwatch__start" @click="start" :v-show="!running || !paused" :disabled="running">
            <svg width="17"
              height="20"
              viewBox="0 0 17 20"
              fill="none"
              xmlns="http://www.w3.org/2000/svg">
              <path d="M0 20V0L17 10L0 20Z" :fill="running ? '#fff' : '#9e9e9e'" />
            </svg>
          </button>
          <button class="stopwatch__pause" @click="pause" v-show="running && !paused" >
            <svg width="10" 
              height="20" 
              viewBox="0 0 10 20" 
              fill="none" 
              xmlns="http://www.w3.org/2000/svg">
              <rect x="7" width="3" height="20" :fill="running ? '#fff' : '#9e9e9e'"/>
              <rect width="3" height="20" :fill="running ? '#fff' : '#9e9e9e'"/>
            </svg>
          </button>
          <button class="stopwatch__stop" @click="stop">
            <svg width="20" 
              height="20" 
              viewBox="0 0 20 20" 
              fill="none" 
              xmlns="http://www.w3.org/2000/svg">
              <rect width="20" height="20" :fill="running ? '#ffffff' : '#9e9e9e'"/>
            </svg>
          </button>
        </div>
      </div>
      <button class="add-btn" @click="addStopwatch">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="8.5" width="3" height="20" fill="#9e9e9e" />
          <rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" fill="#9e9e9e" />
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        running: false,
        paused: false,
        time: 0,
        stopwatches: [],
      }
    },
    methods: {
      start() {
        this.running = true
        this.paused = false
        this.timer = setInterval(() => {
          this.time += 10
        }, 10)
      },
      pause() {
        this.running = false
        this.paused = true
        clearInterval(this.timer)
      },
      stop() {
        this.running = false
        this.paused = false
        clearInterval(this.timer)
        this.time = 0
      },
      addStopwatch(stopwatch) {
        this.stopwatches.push(stopwatch)
      },
      removeStopwatch(stopwatch) {
        this.stopwatches = this.stopwatches.filter(el => el.id !== stopwatch.id)
      }
    },
    computed: {
      formatTime() {
        let hours = Math.floor(this.time / 3600000)
        let minutes = Math.floor(this.time / 60000) % 60
        let seconds = Math.floor(this.time / 1000) % 60
  
        return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`
      }
    }
  }
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
    --primary-bg-color:  #353638;
    --secondary-bg-color: #696969;
  }
  .container {
    background-color: var(--primary-bg-color);
    
  }
  .stopwatch-container {
    font-family: 'Gotham Pro', sans-serif;
    font-weight: 400;
    font-size: 22px;
    line-height: 21px;
    display: grid;
    grid-template-columns: 220px;
    grid-template-rows: auto;
    gap: 50px;
    justify-content: center;
    padding: 70px 0 80px;
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

  .stopwatch {
    background-color: var(--secondary-bg-color);
    /* width: 225px; */
    height: 120px;
    color: #9e9e9e;
    display: flex;
    flex-flow: column nowrap;
    justify-content: space-evenly;
    align-items: center;
  }
  .stopwatch__bar {
    height: 1px;
    width: 100%;
    background-color: #9e9e9e;
  }
  .stopwatch__controls {
    display: flex;
    gap: 50px;
  }

  .is-active {
    color: #fff;
  }

  .white-bg {
    background-color: #fff;
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