
<template>

<div class="container">
  <div id="app">
    
    <h2>Work hard like Elon Musk!!</h2>
    <h3 v-if="onBreak" style="color:green">You're on break, prepare to get back to work!</h3>
      <div class="timer">
        <span class="minute">{{ minutes }}</span>
        <span>:</span>
        <span class="seconds">{{ seconds }}</span>
      </div>
      <div class="controls">
        <div class="start" v-if="!timer" @click="startTimer">
          <i class="fas fa-play fa-2x"></i>
          
        </div>
        
        <div class="pause" v-if="timer" @click="stopTimer">
          
          <i class="fas fa-pause fa-2x"></i>
        </div>
        <div class="stop" v-if="resetButton" @click="resetTimer">
         
          <i class="fas fa-redo-alt fa-2x"></i>
        </div>
        <div class="edit" v-if="!timer" @click="editTimer">
          
          <i class="fas fa-edit fa-2x"></i>
        </div>
      </div>

      <div class="info">
        <div class="session">
          <span>Session: </span><span>{{userTime}}</span>
        </div>
        <div class="session">
          <span>Break: </span><span>{{breakTime}}</span>
        </div>
      </div>
      
        <div class="input">
        <transition name="fade">
        <input type="text" v-if="edit" v-model="userTime">
      </transition>
      </div>

        <div class="input">
        <transition name="fade">
        <input type="text" v-if="edit" v-model="breakTime">
      </transition>
      </div>
      
      
      
    </div>
</div>
</template>

<script>


export default {
  data() {
    return {
      timer: 0,
      totalTime: (25*60),
      resetButton: false,
      onBreak: false,
      edit: false,
      userTime: 25,
      breakTime: 5,
    }
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => this.countdown(), 1000)
        this.resetButton = true
        this.edit = false   
        console.log('hello');
            
    },
    stopTimer() {
      clearInterval(this.timer)
      this.timer = null
      this.resetButton = true
    },
    resetTimer() {
      this.totalTime = (this.userTime * 60);
      clearInterval(this.timer)
      this.timer = null
      this.resetButton = false
      this.onBreak = false
    },
    editTimer() {
      this.edit = !this.edit
    },
    padTime(time) {
      return (time < 10 ? '0' : '') + time
    },
    countdown() {
      this.totalTime--
      if (this.totalTime == 0) {
        this.totalTime = (this.breakTime * 60)
        this.showTitle()
      }
    },
    showTitle() {
      this.onBreak = true
    }
  },
  computed: {
    
    minutes() {
      const minutes = Math.floor(this.totalTime / 60)
      return this.padTime(minutes)
    },
    seconds() {
      const seconds = this.totalTime - (this.minutes * 60)
      return this.padTime(seconds)
    }
  }
  
}
</script>

<style>

h2 {
  color:lavender;
}
.container {
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #0A2132;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#app > * {
  margin-bottom: 2rem;
}

.timer {
  font-size: 9rem;
  color: #EEEEEE;
}

.controls {
    display: flex;
    justify-content: space-evenly;
    width: 100%;
  }

  .info {
    font-size: 2rem;
    color: white;
    display: flex;
    justify-content: space-evenly;
    width: 100%;
  }

 
 .input > input {
      background-color: #393E46;
      border: none;
      font-size: 2rem;
      padding: 1em;
      text-align: center;
      color: white;
    }

  .input > input .fade-enter, .fade-leave-active {
    transition: opacity .5s;
  }
  .input > input .fade-enter, .fade-leave-active {
    opacity: 0;
  }
  i {
    color: #EEEEEE;
    size: 10px;
  }
  i:hover {
    cursor: pointer;
    transform: scale(1.2);
  }
  
</style>
