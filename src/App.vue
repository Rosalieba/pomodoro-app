<template>
 <div class="timer">
  <div class="title">Pomodoro</div>
    <!--https://sabe.io/blog/javascript-convert-milliseconds-seconds-minutes-hours and stackoverflow for the zero before seconds-->
    <p class="clock">{{ Math.floor((workTime / 1000 / 60) % 60) + (Math.floor((workTime / 1000) % 60) < 10 ? (" : 0" + Math.floor((workTime / 1000) % 60))
        : (" : " + Math.floor((workTime / 1000) % 60)))}}</p>
    <div class="input" v-if="showInput">
      <form>
        <label>Work Time in ms </label>
        <input type="number" v-model="workTime"><br>
        <label>Chill Out Time in ms </label>
        <input type="number" v-model="chillOutTime">
      </form>
    </div>
    <div v-if="showWork">
      <div class="buttonContainer">
        <button @click="startWork">Start Work</button>
        <button @click="stopWork">Stop Work</button>
      </div>  
    </div>
    <div v-if="showChillOut" class="pause">
      <div class="buttonContainer">
        <button @click="startChillOut">Start Chill Out</button>
        <button @click="stopChillOut">Stop Chill Out</button>
      </div>
      <p class="clock">{{ Math.floor((chillOutTime / 1000 / 60) % 60) + (Math.floor((chillOutTime / 1000) % 60) < 10 ? (" : 0" + Math.floor((chillOutTime / 1000) % 60))
      : (" : " + Math.floor((chillOutTime / 1000) % 60)))}}</p>
      <p v-if="endChill">End of ChillOut</p>
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
      workTime: null,
      chillOutTime: null,
      showInput: true,
      showWork: true,
      showChillOut: false,
      endChill: false
    }
  },
  methods: {
    startWork() {
      console.log('entering startWork');
      this.showInput = false;
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
       this.workTime = 10000; //how to reset to value entered by user ?
       console.log('Reset to ms: ' + this.workTime);
    },
    startChillOut() {
      this.showInput = false;
      this.timerChill = setInterval(() => {
        console.log('Chill out time setInterval()' + this.timerChill)
        this.chillOutTime -= 1000;
        if (this.chillOutTime <= 0) {
          clearInterval(this.timerChill);
          this.showChillOut = true;
          this.showWork = true;
          this.resetWork();
          this.resetChillOut();
          this.showInput = true;
          this.endChill = true;
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
  width: 25vw;
  height: 30vh;
  border-radius: 20px;
  background: #1BD7DF;
  color: #FFFFF0;
  padding:  5vh 5vw 15vh 5vw;
  margin: 3vh 3vw;
}
.title {
  font-size: large;
  text-transform: uppercase;
  font-weight: bold;
}
.input {
  font-style: italic;
  font-weight: 200;
  padding: 2vh;
}
.buttonContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-around;
}
button {
  background-color:#2c3e50;
  color: white;
  border: 0.3vh solid white;
  border-radius: 0.3vh;
  font-size: 15px;
  padding: 1.5vh;
}
.clock {
  margin: 2vh;
  border: 2px solid white;
  padding: 4vh;
  font-size: 15px;
}
.pause {
  width: 80vw;
  height: 80vh;
  border-radius: 20px;
  color: #FFFFF0;
  padding:  5vh 5vw 15vh 5vw;
  margin: 3vh 3vw;
  background:#ed1dbf
}

</style>