<template>
  <div>
    <div><h3>Game Over</h3></div>
    <button @click="restartGame">Restart</button>
    <h3>Best mark: {{bestScore}}</h3>
  </div>
</template>

<script>
export default {

  props: ['bestScore'],
  methods: {
      restartGame(){this.$emit('restart-game') }
  },
}

</script>

<style scoped>
h3{
    margin-top: 16vh;
    font-size: 1.4rem;
}
button{
    margin-top: 2rem;
    height: 4rem;
    width: 7rem;
    border-radius: 1rem;
    background-color: salmon;
    color: #fff;
    font-size: 1.5rem;
    font-weight: 600;
}
</style>