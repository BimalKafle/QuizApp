<script setup>
import q from './data/quizes'
import {ref, watch} from 'vue'
import Card from './components/QuizCard.vue'

const quizList=ref(q);
const search=ref("");

watch(search,()=>{
  quizList.value=q.filter(quiz=>quiz.name.toLowerCase().includes(search.value.toLowerCase()))
})
</script>

<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search.."/>
    </header>

    <div class="option-container">
      <!-- <div v-for="quiz in quizList"  :key="quiz.id" class="card">
        <img :src="quiz.img" alt="">
        <div class="card-text">
          <h2>{{quiz.name}}</h2>
          <p>{{quiz.questions.length}}</p>
        </div>
      </div> -->
      <Card v-for="quiz in quizList" :key="quiz.id" :quiz="quiz"/>
    </div>
  </div>
</template>


<style scoped>
.container{
  width: 1000px;
  margin:0 auto;
}

header{
  margin-bottom:10px;
  margin-top:30px;
  display: flex;
  align-items: center;
}

header h1{
  font-weight: bold;
  margin-right: 30px;
}

header input{
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
}
.option-container{
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
  justify-content: space-around;
}

</style>