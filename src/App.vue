<template>
 <div class="timer">
  <div class="title">Pomodoro app</div>
    <button @click="startPomo">Start Work</button>
    <button @click="stopPomo">Stop Work</button>
    <button @click="resetPomo">Work Reset Time</button>
    <!--https://sabe.io/blog/javascript-convert-milliseconds-seconds-minutes-hours and stackoverflow for the zero before seconds-->
    <p>{{ Math.floor((pomoTime / 1000 / 60) % 60) + (Math.floor((pomoTime / 1000) % 60) < 10 ? (" : 0" + Math.floor((pomoTime / 1000) % 60))
     : (" : " + Math.floor((pomoTime / 1000) % 60)))}}</p>
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
      pomoTime: 1500500,
      chillOutTime: 300000
    }
  },
  methods: {
    startPomo() {
      console.log('entering startPomo');
      this.timer = setInterval(() => {
          this.pomoTime -= 1000;
        console.log('I am in the setInterval repetition: ' + this.pomoTime);
        if (this.pomoTime <= 0) {
          clearInterval(this.timer);
        }
      }, 1000);
      console.log('I am at the end of the startPomo.')
    },
    stopPomo() {
      clearInterval(this.timer);
      console.log('stopping');
    },
    resetPomo() {
      this.pomoTime = 1500000;
      console.log('Resetted to ms: ' + this.pomoTime);
    },
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