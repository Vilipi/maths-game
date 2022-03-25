<template>
  <div>
    <div class="intro-message">
        <h3>Try to answer as many operation as you can before the timer reaches 0</h3>
    </div>
    <div><button  @click="startGame()">Start</button></div>
  </div>
</template>

<script>
export default {
    methods: {
        startGame(){
            this.$emit('start-game') 
        }
    }
}
</script>

<style scoped>
.intro-message{
    margin: 0.5rem;
}
h3{
    margin-top: 20vh;
    font-size: 1.5rem;
}
button{
    margin-top: 7vh;
    height: 4rem;
    width: 7rem;
    border-radius: 1rem;
    background-color: salmon;
    color: #fff;
    font-size: 1.5rem;
    font-weight: 600;
}
</style>