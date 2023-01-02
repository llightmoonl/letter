<template>
  <div class="question" v-if="checkTest">
    <div class="container">
      <div class="question__content">
        <h1 class = "question__title">{{ data.question }}</h1>
        <p class = "question__explanation">После ответа на вопрос, <br> открывается скрытый текст.</p>
        <div class="question__form">
          <div class="question__input">
            <input class = "input" type="text" v-model="answer" placeholder=" " @keyup.enter = "checkAnswers">
            <label class = "placeholder">Ответ</label>
          </div>
        </div>
      </div>
    </div>
  </div>
  <LetterText :data-json="data" v-if = "checkText"/>
</template>

<script>
import LetterText from './components/LetterText.vue'
const axios = require('axios');

export default {
  name: 'App',
  components: {
    LetterText
  },
  data(){
    return {
      checkText: false,
      checkTest: true,
      answer: "",
      data: {},
      correctAnswer: "",
    }
  },
  methods:{
    checkAnswers(){
      if(((this.answer.toLowerCase()).trim()) === ((this.correctAnswer.toLowerCase()).trim())){
        this.checkText = true;
        this.checkTest = false;
      }
      else{
        let questionForm = document.querySelector('.question__form');
        let questionInput = questionForm.querySelector('.input');
        let questionPlaceholder = questionForm.querySelector('.placeholder');

        questionInput.style.borderColor = "#e70000";
        questionInput.style.outlineColor = "#e70000";
        questionPlaceholder.style.color = "#e70000";
        questionPlaceholder.textContent = "Неправильный ответ";

        setTimeout(() => {
          questionInput.style.borderColor = null;
          questionInput.style.outlineColor = null;
          questionPlaceholder.style.color = null;
          questionPlaceholder.textContent = "Ответ";
        }, 5000);
      }
    }
  },
  mounted() {
    axios
        .get('/data.json')
        .then(response=> {
          this.data = response.data;
          this.correctAnswer = response.data.answerQuestion;
        });
  }
}
</script>
