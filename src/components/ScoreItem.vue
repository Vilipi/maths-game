<template>
  <div>
    <h3>Your score: {{counter}}</h3> 
  </div>
</template>

<script>
export default {
    props: ['counter']
}
</script>

<style scoped>

h3{
    margin-top: 3rem;
    font-size: 1.2rem;
}

</style>