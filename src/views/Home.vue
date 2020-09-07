<template>
<div class="container">
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <h6 class="navbar-brand">Timer - {{min}} Min - {{ sec }} Sec  </h6>
     <span class="ml-auto">{{index+1}}/30</span>
  </nav>
  <div class="container ">
    <div class="row justify-content-center">
      <div class="col-md-6 mt-3 shadow p-3 mb-5 bg-white rounded">
    <div class="card-body ">
      <h5 class="card-title">0{{index+1}}. {{question[index]}} </h5>

      <div class="radio">
        <label><input type="radio" name="optradio" > {{answer1[index]}} </label>
      </div>
      <div class="radio">
        <label><input type="radio" name="optradio"> {{answer2[index]}} </label>
      </div>
      <div class="radio ">
        <label><input type="radio" name="optradio" > {{answer3[index]}} </label>
      </div>
      <div class="radio ">
        <label><input type="radio" name="optradio" > {{answer4[index]}} </label>
      </div>

      <button @click="nextPage()" class="btn btn-primary float-right">Next</button>
    </div>
  </div>

</div>
  </div>
</div>

</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  data(){
    return{
      min  : 29,
      sec  : 60,
      mili : 10,
      question : ['Which is good ?','Good color ?','Which Country is Beautiful ?'],
      answer1  : ['Book','Red','Bangladesh'],
      answer2  : ['Pen','Orange','Nepal'],
      answer3  : ['Bag','Blue','India'],
      answer4  : ['Pencil','White','USA'],
      index    : 0,
    }
  },
  methods:{
      timer(){
       setInterval(()=>{

         if(this.mili >=0){
           this.mili --;
         }

         if(this.sec >= 0 && this.mili === 0){
           this.sec --;
           this.mili = 10;
         }

         if(this.min >= 0 && this.sec === 0){
           this.min --;
           this.sec = 60;
         }
       },100)
     },
    nextPage(){
        if(this.index<2)this.index++;

    },
    },

  mounted() {
    this.timer();
  },
  components: {
    HelloWorld
  }
}
</script>
