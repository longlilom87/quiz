<template>
  <div id="app">
    <Header :correctAnswers = "correctAnswers" :totalAnswers = "totalAnswers"
    />
    <br>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset ="3">
          <QuestionBox
          v-if ="questions.length"
          :numQuestions="questions.length" :questionIndex="index" :currentQuestion="questions[index]" 
          :next="nextQuestion" :previous="previousQuestion" :increment="increment" 
          />
        </b-col>
        
      </b-row>
    </b-container>

  
  </div>
</template>

<script>

import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'


export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data(){ 
    return{
        questions: [],
        index: 0,
        correctAnswers:0,
        totalAnswers: 0
    }
  },
  methods:{
    nextQuestion(){
      this.index++;
    },
    previousQuestion(){
      this.index--;
    },
    increment(isCorrect){
      if (isCorrect){
        this.correctAnswers++;
      }
      this.totalAnswers++;
    }
  },
  mounted: function(){
    // https://opentdb.com/api.php?amount=10&category=26&difficulty=medium&type=multiple
    // https://opentdb.com/api.php?amount=10&category=18&difficulty=medium&type=multiple
      fetch('https://opentdb.com/api.php?amount=20&category=18&difficulty=medium&type=multiple',{
        method: 'get'
      }) .then ((response)=>{
        return response.json()
      })
      .then((jsonData)=>{
        this.questions = jsonData.results
        
      })
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
  

}
</style>
