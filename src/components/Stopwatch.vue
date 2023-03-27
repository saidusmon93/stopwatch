<template>
  <div class="stopwatch">
    <div class="formatTime" :style="{ color: action.color }">
      {{ formatTime }}
    </div>
    <img :src="require(`../assets/img/${action.line}.png`)" />
    <div class="btnAction">
      <div @click="toggle">
        <img :src="require(`../assets/img/${action.play}.png`)" alt="play" />
      </div>
      <div @click="reset">
        <img :src="require(`../assets/img/${action.reset}.png`)" alt="reset" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Stopwatch",
  data() {
    return {
      startTime: null,
      elapsedTime: 0,
      isStart: false,
    };
  },
  computed: {
    action() {
      return {
        reset: this.isStart ? "reset" : "resetOff",
        line: this.isStart ? "Vector" : "VectorOff",
        color: this.isStart ? "#FFFFFF" : "#9E9E9E",
        play: this.isStart ? "pausa" : "play",
      };
    },
    formatTime() {
      let elapsed = Math.floor(this.elapsedTime / 1000);
      let hours = Math.floor(elapsed / 3600);
      let minutes = Math.floor((elapsed - hours * 3600) / 60);
      let seconds = elapsed - hours * 3600 - minutes * 60;
      let timeFormat = "";
      if (hours > 0) {
        timeFormat += `${this.timeFor(hours)}:`;
      } if (minutes > 0) {
        timeFormat += `${this.timeFor(minutes)}:`;
      } else {
        timeFormat += `${this.timeFor(seconds)}`;
      }
      return timeFormat;
    },
  },
  methods: {
    timeFor(num) {
      return num < 10 ? `0${num}` : num;
    },
    toggle() {
      if (this.isStart) {
        this.pause();
      } else {
        this.start();
      }
    },

    start() {
      if (this.isStart) return;
      this.isStart = true;
      this.startTime = performance.now() - this.elapsedTime;
      requestAnimationFrame(this.update);
    },
    pause() {
      if (!this.isStart) return;
      this.isStart = false;
    },
    reset() {
      this.isStart = false;
      this.elapsedTime = 0;
    },
    update(currentTime) {
      if (!this.isStart) return;
      this.elapsedTime = currentTime - this.startTime;
      requestAnimationFrame(this.update);
    },
  },
};
</script>
