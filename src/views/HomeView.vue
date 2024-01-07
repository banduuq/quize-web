<template>
    <main>
      <div class="q-wrap">
        <h1>Simple Queze</h1>
        <div class="Answer" v-if="currentIndex < questions.length">
          <span>{{ currentQuestion.question }}</span>
          <button :class="{select: isSelected(index)}" @click="checkAnswer(index)" 
          v-for="(answer, index) in currentQuestion.answers" :key="index" :disabled="chosen">
            {{ answer.text }}
          </button>
        </div>
        <div v-else>
          <h1>Congratulations!</h1>
          <p>Your Score: {{ score }}/{{ questions.length }}</p>
        </div>
        <button id="next" v-if="chosen" @click="showNext">Next</button>
      </div>
    </main>
</template>
<script>
export default {
  name: 'HomeView',
  components: {},
  data() {
    return {

      questions: [
        {
          question: "1.which is the largest animal in the world?",
          answers: [
            {text: "shark", correct: false},
            {text: "blue whale", correct: true},
            {text: "elephant", correct: false},
            {text: "giraffe", correct: false}
          ]
        },

        {
          question: "2.which is my namme?",
          answers: [
            {text: "cabaas", correct: false},
            {text: "jeylani", correct: false},
            {text: "tesla", correct: false},
            {text: "qoryooley", correct: true}
          ]
        },
        {
          question: "3.which is my surname?",
          answers: [
            {text: "yavşak jey", correct: false},
            {text: "gt", correct: true},
            {text: "banduuq", correct: false},
            {text: "yavşak cabbas", correct: false}
          ]
        }
      ],
      
      chosen: false,
      currentIndex: 0,
      score: 0,
      selectedIndex:null
    };
  },

  methods: {
    checkAnswer(index){
      this.selectedIndex = index;
      if (this.currentQuestion.answers[index].correct) {
      this.score++;
       }
      this.chosen = true;
    },
    showNext(){
      this.selectedIndex = null; 
        this.currentIndex++;
      this.chosen = false;
    },
    isSelected(index){
      return this.selectedIndex === index;
    }
  },
  computed: {
    currentQuestion() {
        return this.questions[this.currentIndex];
    },
  },
};
</script>

<style>
main{
 width: 100%;
 height: 100vh;
 background-color: #354152;
 display: flex;
 justify-content: center;
 align-items: center;
}
.Answer .select{
  background: #6d44b8;
}

p{
  font-size: 30;
  font-weight: 700;
}
#next{
 width: 150px;
 margin-top: 10px;
 border-radius: 5px;
 text-align: center;
 display: block;
 margin: 10px auto; 
}
.q-wrap{
  width: 600px;
  background: white;
  padding: 20px;
}
.q-wrap h1{
  text-align: center;
}
.q-wrap span{
  font-size: 30px;
  font-weight: 600;
}
.q-wrap button{
 padding: 15px;
 text-align: start;
 background: #354152; 
 color: white;
 font-size: 20px;
 border-radius: 10px;
}
.q-wrap button:hover{
  background: #6d44b8;
}
.Answer{
 display: flex;
 flex-direction: column;
 gap: 10px;
 
}
</style>
