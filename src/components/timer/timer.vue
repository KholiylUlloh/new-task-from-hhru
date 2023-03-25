<template>
  <div class="stopwatch" :class="{ active: status }">
    <div class="time">
      <div v-if="formattedTime.length" id="time">{{ formattedTime }}</div>
      <div v-if="!formattedTime.length" id="time">{{ 0 }}</div>
    </div>
    <div class="btns">
      <img
        @click="start"
        v-if="isStopped"
        src="../../assets/play.svg"
        alt="play"
      />
      <img
        @click="pause"
        v-else="!isStopped"
        src="../../assets/pause.svg"
        alt="pause"
      />
      <img
        @click="stop"
        v-if="!status"
        src="../../assets/stop.svg"
        alt="stop"
      />
      <img
        @click="stop"
        v-else="status"
        src="../../assets/stopwhite.svg"
        alt="stop"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentTime: 0,
      formattedTime: "",
      isStopped: true,
      status: false,
      ticker: undefined,
      isRunning: false,
    };
  },
  methods: {
    start() {
      if (!this.isRunning) {
        this.tick();
        this.isStopped = false;
        this.status = true;
        this.isRunning = true;
      }
    },
    pause() {
      window.clearInterval(this.ticker);
      this.status = false;
      this.isStopped = true;
      this.isRunning = false;
    },
    stop() {
      window.clearInterval(this.ticker);
      this.status = false;
      this.isStopped = true;
      this.isRunning = false;
      this.currentTime = 0;
      this.formattedTime = "0";
    },
    tick() {
      this.ticker = setInterval(() => {
        this.currentTime++;
        this.formatTime(this.currentTime);
      }, 1000);
    },
    setZero(num) {
      if (num >= 0 && num < 10) {
        return `0${num}`;
      }
      return num;
    },
    formatTime(sec) {
      let countedTime = new Date(null);
      countedTime.setSeconds(sec);
      let time = countedTime.toISOString().substr(11, 8).replace(/:/gi, ""),
        hours = parseFloat(time.substr(0, 2)),
        minutes = parseFloat(time.substr(2, 2)),
        seconds = parseFloat(time.substr(4, 2));
      if (hours > 0) {
        return (this.formattedTime = `${this.setZero(hours)}:${this.setZero(
          minutes
        )}:${this.setZero(seconds)}`);
      } else if (minutes > 0) {
        return (this.formattedTime = `${this.setZero(minutes)}:${this.setZero(
          seconds
        )}`);
      } else {
        return (this.formattedTime = `${this.setZero(seconds)}`);
      }
    },
  },
};
</script>

<style>
.stopwatch {
  width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  flex-direction: column;
  font-family: "Gotham Pro";
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
}
.time {
  border-bottom: 1px solid #9e9e9e;
  width: inherit;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 60px;
  color: #9e9e9e;
}
#time {
  width: 100%;
  text-align: center;
}
.btns {
  width: inherit;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 48px;
  height: 60px;
}
img {
  cursor: pointer;
}
.active .time {
  color: #ffffff;
  border-bottom-color: #ffffff;
}
</style>
