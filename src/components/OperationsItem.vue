<template>
  <div>
      <h3>{{number1}} {{operator}} {{number2}}</h3>
      <div>
          <!-- <h3>Result : {{result}}</h3>  -->
      </div>
      <div>
          <ul>
              <li v-for="button in buttons" :key="button.index">
                 <button @click="checkAnswer(button)">{{button}}</button> 
              </li>
          </ul>
      </div>
  </div>
</template>

<script>
export default {
    props: ['number1','number2', 'result'],
    data: function(){ // Can't use  the prop item for our v-model so we need to use a new one that is equal to item
        return{
            buttons: [],
            operations: ['+','-','*'],
            operator: ''
        }
    },
    created(){
        this.generateAnswers(),
        this.generateOperator()
    },
    watch: {
        //Cheking when result changes
        result: function(){
            this.generateAnswers()
            this.generateOperator()

        }
    },
    methods: {
        generateOperator(){
            //Including Division
            if(this.number1 > this.number2 && this.number1 % this.number2 === 0){
                this.operator = "/"
            } else {
            //Or random operation from out array    
            this.operator = this.operations[Math.floor(Math.random() * this.operations.length)]
            this.$emit('change-operator', this.operator) 
            }
        },
        generateAnswers(){
            let answers = []
            let result = this.result 
            let random1 = Math.floor(Math.random() * 20 + result)
            // let random2 =  Math.floor(Math.random() * 10 - result)
            let random2 =  random1 + 2
            // let random2 =  Math.floor(Math.random() * 10 - result)
            let random3 = random1 -10
            
            answers.push(random1,random2,random3,result)
            //Shuffle answers
            for (let i = answers.length - 1; i > 0; i--) {
                let j = Math.floor(Math.random() * (i + 1));
                let temp = answers[i];
                answers[i] = answers[j];
                answers[j] = temp;
            }
            this.buttons = answers
            //console.log(this.buttons) 
        },

        checkAnswer(button){
            if(button === this.result){
                this.$emit('change-numbers') 
                console.log('Correct')
            } else {
                this.$emit('fail') 
                console.log('Incorrect')
            }   
        }
        
    }
}
</script>

<style scoped>

h3{
   font-size: 1.4rem;
}
ul {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  list-style: none;
  /* check padding */
  padding: 0;
  overflow: hidden;
  background-color: #333333; 
  

}
li {
  float: left;
  margin: 1.5rem;
}

li button{
  display: block;
  width: 9rem ;
  height: 9rem;
  border-radius: 15px;  
  color: #fff;
  background-color: salmon;
  text-align: center;
  padding: 16px;
  font-size: 2.5rem;
}

@media only screen and (max-width: 600px) {
  li button{
    width: 7rem ;
    height: 7rem;
    font-size: 2rem;
  }
}
</style> 