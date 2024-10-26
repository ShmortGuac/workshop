<script setup>
import { ref, onMounted } from 'vue';
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');
const title = ref("");
const desc = ref("");
const readTask = ref([]);

async function submit(){
  const data = {
    "title": title.value,
    "description": desc.value,
  };
  
  await pb.collection('posts').create(data);
  readTask.value.push(data);
  console.log(readTask);
}

onMounted(async () => {
  const record = await pb.collection('posts').getFullList();
  readTask.value = record;
});

</script>

<template>
  <body class="h-screen bg-zinc-900">
    <p class="text">Shmort's To Do List</p>    
    <div class="div1 grid-cols-2 gap-2">
      <input class="taskbox" type="text" placeholder="Enter your task" v-model="title">
      <input class="descbox" type="text" placeholder="Describe your task" v-model="desc">
      <button class="button" @click="submit">CREATE TASK</button>
    </div>
    <br>
    <button class="task" v-for="item in readTask">
      {{ item.title }}
    </button>
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
  /*outline: 2px solid white;*/
  align-content: center;
}

.div2{
  outline: 2px solid white;
  align-content: center;
}


.taskbox{
  margin-bottom: 7px;
  margin-left: auto;
  margin-right: auto;
  display: block;
  font-size: 16px;
  padding: 10px;
  padding-left: 25px;
  width: 40%;
  max-width: 40%;
  border-radius: 999999px;
  background-color: rgb(39 39 42);;
  color: rgb(248 250 252);
  outline: 0px;
  filter: drop-shadow(0 25px 25px rgb(0 0 0 / 0.15));
}

.descbox{
  margin-bottom: 10px;
  margin-left: auto;
  margin-right: auto;
  display: block;
  font-size: 16px;
  padding: 10px;
  padding-left: 25px;
  width: 40%;
  max-width: 40%;
  height: 70px;
  border-radius: 20px;
  background-color: rgb(39 39 42);;
  color: rgb(248 250 252);
  outline: 0px;
  filter: drop-shadow(0 25px 25px rgb(0 0 0 / 0.15));
}

.button{
  margin-left: auto;
  margin-right: auto;
  display: block;
  font-size: 16px;
  padding: 2px;
  height: 30px;
  width: 40%;
  max-width: 40%;
  border-radius: 999999px;
  background-color: rgb(238, 102, 166);;
  color: rgb(248 250 252);
  outline: 0px;
  filter: drop-shadow(0 25px 25px rgb(0 0 0 / 0.15));
  transition: 0.1s;
}

.button:active{
  transform: scale(0.95);
}

.task{
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
  margin-bottom: 10px;
  text-align: center;
  padding: 10px;
  font-size: 20px;
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
