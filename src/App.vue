<template>
 <div class="timer">

  <div class="title">Pomodoro app</div>

  <button @click="startPomo">Start</button>
  <button @click="stopPomo">Stop</button>
  <button @click="resetPomo">Reset Time</button>

  <p>{{ pomoTime }}</p>

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
      pomoTime: 10000,
    }
  },
  methods: {
    startPomo() {
      console.log('entering startPomo');
      this.timer = setInterval(() => {
        console.log('before the while');
        do {
          this.pomoTime -= 1000;
        } while (this.pomoTime < 0);
        console.log('I am in the startPomo method: ' + this.pomoTime);
      }, 1000);
      console.log('I am at the end of the startPomo.')
    },
    stopPomo() {
      clearInterval(this.timer);
      console.log('end of stopPomo: ' + this.timer);
    },
    resetPomo() {
      console.log('entering resetPomo method.');
      this.pomoTime = 10000;
      console.log('end of reset: ' + this.pomoTime);
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