<script setup>
import { ref, onMounted } from 'vue';
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');
const wyrather = ref([]);

let choice = ref(0)
let index = ref(0)


onMounted(async () => {
  const record = await pb.collection('questions').getFullList();
  wyrather.value = record;
});



</script>

<template>
  <body class="h-screen bg-zinc-900">
    <p class="text">Would You Rather?</p>
    <div v-if="wyrather.length == 0"   >Loading.....</div> 
    <div v-else class="div1">
      <button class="option1" @click = "choice=1"><p v-if="choice==1">{{ wyrather[index].chosen_1 }}% would rather</p>{{ wyrather[index].option_1}}</button>
      <button class="option2" @click = "choice=1"><p v-if="choice==1">{{ wyrather[index].chosen_2 }}% would rather</p>{{ wyrather[index].option_2 }}</button>
      
    </div>
    <button class="task" v-if="choice==1" @click = "index++; choice=0; if (index == wyrather.length) {index = 0}">Click Here for next question </button>
  </body>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.text{
  font-size: 3rem;
  font-weight: 700;
  font-family: sans-serif;
  line-height: 1;
  color: rgb(248 250 252);
  text-align: center;
  padding-top: 5rem;
  padding-bottom: 2rem;
}

.div1{
  display: flex;
  gap: 20px;
  justify-content: center;
}

.option1{

  display: block;
  font-size: 40px;
  padding: 2px;
  height: 30rem;
  width: 30rem;
  background-color: rgb(13, 146, 244);
  border-radius: 30px;
  color: rgb(248 250 252);
  outline: 0px;
  filter: drop-shadow(0 25px 25px rgb(0 0 0 / 0.15));
  transition: 0.1s;
}

.option2{
  display: block;
  font-size: 40px;
  padding: 2px;
  height: 30rem;
  width: 30rem;
  background-color: rgb(198, 46, 46);
  border-radius: 30px;
  color: rgb(248 250 252);
  outline: 0px;
  filter: drop-shadow(0 25px 25px rgb(0 0 0 / 0.15));
  transition: 0.1s;
}

.option1:active{
  transform: scale(0.95);
}

.option1:hover{
  rotate: -3deg;
}

.option2:active{
  transform: scale(0.95);
}

.option2:hover{
  rotate: 3deg;
}
.task{
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
  margin-bottom: 10px;
  text-align: center;
  padding: 10px;
  font-size: 16px;
  color: rgb(248 250 252);
  border-style:solid ;
  border-color: rgb(248 250 252);
  border-width: 2px;
  border-radius: 10px;
  width: 40%;
  max-width: 40%;
  transition: 0.3s;
}

.task:hover{
  background-color: rgb(248 250 252);
  color:rgb(24 24 27);
  scale: 1.05;
}

</style>
