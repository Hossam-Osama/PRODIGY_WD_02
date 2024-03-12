<template>
<div class="stopwatch-background">
 <div class="stopwatch-container">
    <h1 class="stopwatch-time" id="color">{{ currentTime }}</h1>
    <div class="stopwatch-controls">
      <button @click="startStopwatch" onclick="document.getElementById('color').style.color='chartreuse'" v-if="!isRunning" class="start-button">Start</button>
      <button @click="pauseStopwatch" onclick="document.getElementById('color').style.color='red'" v-else class="pause-button">Pause</button>
      <button @click="restartStopwatch" class="restart-button">Restart</button>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'hoMe',
  components: {
  },
  data() {
    return {
      isRunning: false,
      startTime: null,
      currentTime: 0,
      pausedTime: 0,
    };
 
  },
  
  methods: {
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now() - this.pausedTime;
        this.updateTime();
      }
    },
    pauseStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        this.pausedTime = Date.now() - this.startTime;
      }
    },
    restartStopwatch() {
      this.isRunning = false;
      this.pausedTime = 0;
      this.currentTime = 0;
    },
    updateTime() {
      if (this.isRunning) {
        const currentTime = Date.now() - this.startTime;
        this.currentTime = Math.floor(currentTime / 1000); // Convert to seconds
        requestAnimationFrame(this.updateTime);
      }
    }

  },
};




</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.stopwatch-background {
  background-image: url('https://th.bing.com/th/id/R.53e7cc23e4f7278c1574c0c9c3490645?rik=Tgi3HtvmfAk5WQ&pid=ImgRaw&r=0');
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.stopwatch-container {
  text-align: center;
  margin-top: 50px;
}

.stopwatch-time {
  font-size: 48px;
  margin-bottom: 20px;
 color: #2196f3 ;
}

.stopwatch-controls {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.start-button,
.pause-button,
.restart-button {
  padding: 10px 20px;
  font-size: 18px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.start-button:hover,
.pause-button:hover,
.restart-button:hover {
  background-color: #45a049;
}

.start-button:focus,
.pause-button:focus,
.restart-button:focus {
  outline: none;
}

.pause-button {
  background-color: #f44336;
}

.restart-button {
  background-color: #2196f3;
}
</style>
