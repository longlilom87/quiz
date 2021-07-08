<template>
    <div class="question-box-container"> 
        <b-jumbotron>

            <template #lead>
              <h1>Question {{questionIndex +1}}</h1>
              {{currentQuestion.question}}
            </template>
        
            <hr class="my-4">

            <b-list-group v-for= "(answer,index) in shuffledAnswers" :key="index">
              <!-- <b-list-group-item 
              @click="selectAnswer(index)" :class="!answered && selectedIndex === index ? 'selected':
              answered && selectedIndex === index ? correctIndex === index? 'correct':'incorrect' : ''">
              {{answer}}
            </b-list-group-item> --> 
            <b-list-group-item 
            @click="selectAnswer(index)" :class="answerClass(index)">
            {{answer}}
          </b-list-group-item>
            </b-list-group>
            
            <b-button @click="previous" variant="success" :disabled="questionIndex==0">&lsaquo;</b-button> <!-- previous -->
            <b-button variant="primary" @click="submitAnswer" :disabled="selectedIndex==null || answered">Choose!</b-button>
            <b-button @click="next" variant="success" :disabled="questionIndex==numQuestions-1">&rsaquo;</b-button> <!-- next -->
            <br>
           
            
        </b-jumbotron>
      </div>
  </template>
  
  <script>
    import _ from 'lodash'
    import {decode} from 'html-entities'
 export default{
   props:{
     numQuestions:Number,
     questionIndex:Number,
     currentQuestion: Object,
     next: Function,
     previous: Function,
     increment: Function
   },
   data:function(){
     return {
        selectedIndex: null,
        shuffledAnswers: [],
        correctIndex: null,
        answered: false
     }
   },
   
   watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null
        this.answered = false
        this.shuffleAnswers()
      }
    }
  },
   methods:{
     selectAnswer(index){
        this.selectedIndex=index
     },
     shuffleAnswers(){ //shuffle and encoding HTML entities in answers
       this.currentQuestion.question = decode(this.currentQuestion.question)
       let answers= [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
       this.shuffledAnswers = _.shuffle(answers)
       for (let i =0; i<this.shuffledAnswers.length;i++){
         this.shuffledAnswers[i]=decode(this.shuffledAnswers[i])
       }
       this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
     },
     answerClass(index){
        let answerClass = ''
        if (!this.answered && this.selectedIndex === index ) answerClass=  'selected'
        else if (this.answered && this.correctIndex === index) answerClass ='correct'
        else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) answerClass ='incorrect'
        return answerClass

     },
     submitAnswer(){ // find the right answer and increasing the counter
       let isCorrect = false
       if (this.selectedIndex === this.correctIndex){
         isCorrect = true
       }
       this.answered = true
       this.increment(isCorrect);
     }
   }
 }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  .list-group{
    margin-bottom: 15px;
  }
  .list-group-item:hover{
    /* background: rgb(113, 155, 179); */
    cursor: pointer;
  }
  .btn{
    margin: 0 5px;
  }
  .selected{
    background-color: blue;
    color:white
  }
  .correct{
    background-color: green;
    color:white
  }
  .incorrect{
    background-color: red;
    color:white
  }

  </style>
  