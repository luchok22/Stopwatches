<template>
  <div class="watch" v-for="(stopwatch, index) in stopwatches" :key="index">
    <div class="time">
      <span :class="stopwatch.running ? 'active' : 'nonActive'">{{
        displayTime(stopwatch.time)
      }}</span>
    </div>
    <hr :class="stopwatch.running && 'activeHR'"/>
    <div class="wrapper-btns">
      <div class="btns">
        <img
          :class="stopwatch.running && 'activeImg'"
          :src="
            stopwatch.running
              ? './stopWatch.svg'
              : './runningWatch.svg'
          "
          @click="joinBtn(stopwatch)"
        />
      </div>
      <div class="btns">
        <img
          :class="stopwatch.running && 'activeImg'"
          src="./resetWatch.svg"
          @click="resetStopwatch(stopwatch)"
          alt="reset"
        />
      </div>
    </div>
  </div>
  <div class="add" @click="addStopwatch">
    <img
    src="./addWatch.svg"
      alt="add"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      stopwatches: [],
    }; 
  },
  methods: {
    addStopwatch() {
      this.stopwatches.push({
        time: 0,
        running: false,
        intervalId: null,
      });
    },
    joinBtn(stopwatch) {
      if (stopwatch.running) {
        clearInterval(stopwatch.intervalId);
        stopwatch.running = false;
      } else {
        stopwatch.intervalId = setInterval(() => {
          stopwatch.time += 1;
        }, 1000);
        stopwatch.running = true;
      }
    },
    resetStopwatch(stopwatch) {
      clearInterval(stopwatch.intervalId);
      stopwatch.time = 0;
      stopwatch.running = false;
    },
    padZero(number) {
      return number < 10 ? `0${number}` : `${number}`;
    },
    displayTime(time) {
      let hours = Math.floor(time / 3600);
      let minutes = Math.floor((time - hours * 3600) / 60);
      let seconds = time - hours * 3600 - minutes * 60;

      if (hours > 0) {
        return `${hours}:${this.padZero(minutes)}:${this.padZero(seconds)}`;
      } else if (minutes > 0) {
        return `${minutes}:${this.padZero(seconds)}`;
      } else {
        return `${seconds}`;
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
/* stopwhatch */
.watch {
  height: 120px;
  display: flex;
  flex-direction: column;
  background: #696969;
  opacity: 0;
  animation: show 1s forwards;
}
@keyframes show {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
/* end */

/* time */
.time {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px 70px;
}
hr {
  margin-bottom: 20px;
  border: 1px solid #9e9e9e;
}
.time span {
  font-family: "Gotham Pro";
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  text-align: center;
}
/* end */

/* btns */
.wrapper-btns {
  display: flex;
  justify-content: space-around;
  padding: 0px 70px;
  gap: 50%;
}
.btns img {
  width: 20px;
}
/* end */

/* addWatch */
.add {
  height: 120px;
  background: #696969;
  display: flex;
  justify-content: center;
  align-items: center;
}
.add img {
  width: 20px;
}
/* end */

/* active */
.wrapper-active {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 50px;
}
.wrapper-active span {
  color: red;
}
/* end */

/* active */
.active {
  color: #ffffff;
  transition: 0.2s;
}
.activeHR {
  transition: 0.5s;
  border: 1px solid #ffffff;
}
.nonActive {
  color: #9e9e9e;
}
.activeImg {
  filter: brightness(0) saturate(100%) invert(1);
}

/* end */
</style>
