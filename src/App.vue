<script setup>
import { ref } from 'vue'

let newTask = ref('')
let taskList = ref([
  { text: 'Estudiar', done: false },
  { text: 'Jugar Play', done: true }
])

function addTask(){
  if(newTask.value.trim() === '') return
  taskList.value.push({
    text: newTask.value,
    done: false
  })
  newTask.value = '';
}

function setDone(index){
  taskList.value[index].done = !taskList.value[index].done
  
  
}
function deleteTask(index){
taskList.value.splice(index,1);
}
</script>

<template>
  .
  <div class="card">
    <h1>Lista de cosas</h1>
    <p class="subtitle">{{ newTask }}</p>
    <div>
      <div v-for="(task,index) in taskList" :key="index" class="task" :class="{ done: task.done }">{{ task.text }} <span @click="setDone(index)" @dblclick="deleteTask(index)"  class="button">x</span></div>
    </div>
    <div>
      <input v-model="newTask" @keypress.enter=" addTask" type="text" placeholder="Escribe tu tarea" />
      <p class="help" v-show="newTask != ''">Presiona Enter para confirmar</p>
    </div>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
  
}
.subtitle {
  padding: 0;
  margin: 0;
  text-align: center;
  opacity: 0.6;
}
* {
  font-family: 'Hanken Grotesk', sans-serif;
  box-sizing: border-box;
}
h1 {
  text-transform: uppercase;
  text-align: center;
  padding: 0;
  margin: 0;
  font-size: 24px;
}
.card {
  background-color: #e6e8e6;
  max-width: 520px;
  border-radius: 8px;
  padding: 18px 16px;
  margin: 0 auto;
  overflow: hidden;
}
.task {
  background-color: #df2935;
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
  padding-right: 2px;
}
.task:hover {
  background-color: #fe6d73;
}
.button {
  display: flex;
  background-color: #f7fff7;
  color: #df2935;
  padding: 0 5px;
  border-radius: 2px;
  align-items: center;
}
.button:hover {
  cursor: pointer;
  background-color: #ffc2d1;
  color: white;
}
input {
  width: 100%;
  border: none;
  outline: none;
  padding: 3px 6px;
  border-radius: 4px;
}
.help {
  margin: 0;
  font-size: 12px;
  opacity: 0.4;
  padding-top: 10px;
}
</style>
