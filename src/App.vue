<template>
 <div class="timer">
  <div class="title">Pomodoro app</div>
  <form>
    <label>Work Time in ms</label>
    <input type="number" v-model="workTime"><br>
    <label>Chill Out Time in ms</label>
    <input type="number" v-model="chillOutTime">
  </form>
    <div v-if="showWork">
      <button @click="startWork">Start Work</button>
      <button @click="stopWork">Stop Work</button>
      <button @click="resetWork">Reset Work</button>
      <!--https://sabe.io/blog/javascript-convert-milliseconds-seconds-minutes-hours and stackoverflow for the zero before seconds-->
      <p>{{ Math.floor((workTime / 1000 / 60) % 60) + (Math.floor((workTime / 1000) % 60) < 10 ? (" : 0" + Math.floor((workTime / 1000) % 60))
      : (" : " + Math.floor((workTime / 1000) % 60)))}}</p>
    </div>
    <div v-if="showChillOut">
      <button @click="startChillOut">Start Chill Out</button>
      <button @click="stopChillOut">Stop Chill Out</button>
      <button @click="resetChillOut">Chill Out Reset Time</button>
      <p>{{ Math.floor((chillOutTime / 1000 / 60) % 60) + (Math.floor((chillOutTime / 1000) % 60) < 10 ? (" : 0" + Math.floor((chillOutTime / 1000) % 60))
      : (" : " + Math.floor((chillOutTime / 1000) % 60)))}}</p>
    </div>
 </div> 
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      timer: null,
      timerChill: null,
      workTime: 10000,
      chillOutTime: 5000,
      showWork: true,
      showChillOut: false
    }
  },
  methods: {
    startWork() {
      console.log('entering startWork');
      this.showWork = true;
      this.showChillOut = false;
      this.timer = setInterval(() => {
          this.workTime -= 1000;
        console.log('I am in the setInterval repetition: ' + this.workTime);
        if (this.workTime <= 0) {
          clearInterval(this.timer);
          this.showWork = false;
          this.showChillOut = true;
          this.startChillOut();
        }
      }, 1000);
      console.log('I am at the end of the startWork.')
    },
    stopWork() {
      clearInterval(this.timer);
      console.log('stopping');
    },
    resetWork() {
      this.workTime = 10000;
      console.log('Reset to ms: ' + this.workTime);
    },
    startChillOut() {
      this.timerChill = setInterval(() => {
        console.log('Chill out time setInterval()' + this.timerChill)
        this.chillOutTime -= 1000;
        if (this.chillOutTime <= 0) {
          clearInterval(this.timerChill);
          this.showChillOut = false;
          this.showWork = true;
          this.resetWork();
          this.resetChillOut();
        }
      }, 1000)
    },
    stopChillOut() {
      clearInterval(this.timerChill);
      console.log('stopping chill out');
    },
    resetChillOut() {
      this.chillOutTime = 5000;
      console.log('Reset chill out to ms: ' + this.chillOutTime);
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.timer {
  width: 400px;
  border-radius: 20px;
  background: #182bba;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}

.title {
  vertical-align: top;
}
</style>