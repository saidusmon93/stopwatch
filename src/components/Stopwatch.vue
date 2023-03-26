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
      <div @click="reset" :disabled="!time">
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
      time: 3599,
      isStart: false,
      timerId: null,
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
      let hours = Math.floor(this.time / 3600);
      let minutes = Math.floor((this.time - hours * 3600) / 60);
      let seconds = this.time - hours * 3600 - minutes * 60;
      let timeFormat = "";
      if (hours > 0) {
        timeFormat += `${this.timeFor(hours)}:`;
      }
      if (minutes > 0) {
        timeFormat += `${this.timeFor(minutes)}:`;
      }
      timeFormat += `${this.timeFor(seconds)}`;
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
      if (this.isStart) {
        return;
      }
      this.isStart = true;
      this.timerId = setInterval(() => {
        this.time++;
      }, 1000);
    },
    pause() {
      if (!this.isStart) {
        return;
      }
      clearInterval(this.timerId);
      this.isStart = false;
    },
    reset() {
      if (this.isStart) {
        clearInterval(this.timerId);
      }
      this.time = 0;
      this.isStart = false;
    },
  },
};
</script>
