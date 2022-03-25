<template>
<div>
     <h3>{{this.time}}</h3>
</div>  
</template>

<script>
export default {
    props: ['timer','counter'],

    data: function(){ 
        return{
            time: this.timer

        }
    },
    mounted() {
        // this.time = this.timer
        window.setInterval(() => {
            if(this.time > 0){
            this.$set(this, 'time', this.time - 1)
            }
        }, 1000)

    },
    watch: {
        //Cheking when this.time changes and check if it is 0
        time: function(){
            /////////////ACTIVAR PARA JUGAR/////////////
            this.finalCountdown() 
        },
        counter: function(){
            this.time += 3
        }
    },
    methods: {
        finalCountdown(){
            if (this.time === 0){
                this.$emit('final-time') 
                this.time = 10
            }
        }
    }
}
</script>

<style>

</style>