<template>
  <div id="app">
    <h1>Maths game</h1>
    <IntroMessage
      v-if="introScreen"
      @start-game="onStartGame">
    </IntroMessage>
    <FailMessage
      v-if="endGame"
      @restart-game="onRestartGame"
      :bestScore="bestScore">  
    </FailMessage>
    <ScoreItem
      v-if="!introScreen"
      :counter="counter">
    </ScoreItem>
    <OperationsItem
      v-if="gameElements"
      :number1="number1"
      :number2="number2"
      :result="result"
      @change-numbers="onChangeNumbers"
      @change-operator="createResult"
      @fail="onFail">
    </OperationsItem>
    <TimerItem
      v-if="gameElements"  
      :timer="timer"
      :counter="counter"
      @final-time="onFail">
    </TimerItem>
  </div>
</template>

<script>

import OperationsItem from './components/OperationsItem.vue'
import FailMessage from './components/FailMessage.vue'
import ScoreItem from './components/ScoreItem.vue'
import TimerItem from './components/TimerItem.vue'
import IntroMessage from './components/IntroMessage.vue'


export default {
  name: 'App',
  components: {
    OperationsItem,
    FailMessage,
    ScoreItem,
    TimerItem,
    IntroMessage
  },
  data(){
    return{
      number1: 1,
      number2: 1,
      result: 0,
      introScreen: true,
      endGame: false,
      gameElements: false,
      counter: 0,
      bestScore: 0,
      timer: 10   
    }
  },
  methods: {
    onChangeNumbers(){
      this.number1 = Math.floor(Math.random() * 20)
      this.number2 = Math.floor(Math.random() * 20)
      //console.log(`${this.number1} ${this.number2}`)
      this.createResult()
      this.counter++
    },
  
    createResult(operator){
      // console.log(operator)
      // console.log(this.result)
      if(operator === '+'){
        this.result = this.number1 + this.number2
      } else if (operator === '-'){
        this.result = this.number1 - this.number2
      } else if (operator === '*'){
        this.result = this.number1 * this.number2
      } else {
      // console.log(operator)
        this.result = this.number1 / this.number2
      }

    },
    onFail(){
      this.endGame = true  
      this.gameElements = false
      this.bestScore = JSON.parse(localStorage.getItem('bestCounter'))
      if(this.bestScore < this.counter){
        this.bestScore = this.counter
        localStorage.setItem('bestCounter', JSON.stringify(this.counter))
        console.log(localStorage.getItem('bestCounter'))
      }
      
    },
    onRestartGame(){
      this.gameElements = true
      this.endGame = false
      //Generating New Values
      this.onChangeNumbers()
      this.createResult()
      this.counter = 0
    },
    onStartGame(){
      this.introScreen = false
      this.gameElements = true
    }
  },
  created(){
      this.createResult()
  },
}
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
