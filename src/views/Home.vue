<template>
  <div class="container" v-if="question.length">
    <nav class="navbar navbar-expand-lg navbar-light bg-light shadow p-3  bg-white rounded">
      <h6 class="navbar-brand">Timer - {{ min }} Min - {{ sec }} Sec </h6>
      <span class="ml-auto">{{ question_index + 1 }}/{{ question.length }}</span>
    </nav>

    <div v-if="!kee_press" class="container ">
      <div class="row justify-content-center">
        <div class="col-md-8 mt-3 shadow p-3 mb-5 bg-white rounded">
          <div class="card-body">
            <h3 class="question-title mb-4"> Q{{ question_index + 1 }}: {{ question[question_index].question }}</h3>
            <div>
              <div class="custom-control " v-for="(answer,index) in question[question_index].answers "
                   :class="'custom-'+ question[question_index].type">
                <input :type="question[question_index].type" :id="index" class="custom-control-input"
                       v-model="question[question_index].checked"
                       :value="answer">
                <label class="question-answer custom-control-label " :for="index">{{ answer.title }}</label>
              </div>
            </div>
            <button v-if="!btn" @click="nextPage()" class="btn btn-primary float-right mt-4">Next</button>
            <button v-else @click="result()" class="btn btn-success float-right mt-4">Submit</button>
          </div>
        </div>
      </div>
    </div>

    <div v-else>
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-md-6 mt-3 shadow p-3 mb-5 bg-white rounded">
            <h5> You are Pressed on keyboard.To continue Exam press Ok.</h5>
            <button @click="kee_press = false" class="btn btn-success float-right mt-4">Ok</button>
          </div>
        </div>
      </div>
    </div>

  </div>

</template>

<script>
// @ is an alias to /src
import data from '../data/question.json'

export default {
  name: 'Home',
  data() {
    return {
      min: 29,
      sec: 60,
      question: [],
      option: '',
      question_index: 0,
      answer: 0,
      kee_press: false,
      btn: false,
    }
  },
  methods: {
    timer() {
      setInterval(() => {

        if (this.sec >= 0) {
          this.sec--;
        }

        if (this.min >= 0 && this.sec === 0) {
          this.min--;
          this.sec = 60;
        }

       // if (this.min === 28)this.result();
      }, 1000)
    },
    nextPage() {
      console.log(this.answer)
      if (this.question_index < this.question.length - 1) {
        this.question_index++;
      }
      if (this.question_index === this.question.length - 1) {
        this.btn = true;
      }

    },
    keyListen(event) {
      event.preventDefault();
      this.kee_press = true;
    },
    result(){
      alert('Your exam is Submitted');
    }
  },

  mounted() {
    this.question = data.exam;
    console.log(this.question);
    this.timer();
     window.addEventListener('keydown', this.keyListen)
  /*   window.addEventListener('contextmenu', function (e) {
      e.preventDefault();
    });*/
  },
}
</script>
