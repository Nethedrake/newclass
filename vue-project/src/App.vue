<script setup>
import { ref } from 'vue';

let newtask = ref('')
let tasklist = ref([
  {
  text : 'Estudiar', done:false
}, 
{
  text: 'Jugar Play', done:true
  }])

  function setDone(index){
    tasklist.value[index].done = !tasklist.value[index].done
   
  }
  function deletetask(index){
    tasklist.value.splice(index,1)
  }



  function addtask(){
    if(newtask.value.trim()=='')return
    tasklist.value.push({
      text: newtask.value,
      done: false
    })
    newtask.value = ''
  }
</script>
<template>
  <div class="card">
    <h1>Lista de cosas</h1>
    <p class="subtittle">{{ newtask }}</p>
    <div>
      <div v-for=" (task,index) in tasklist " :key="index" class="task " :class="{done:task.done }">{{ task.text }}<span @dblclick="deletetask(index)" @click="setDone(index)" class="button">x</span></div>
      <div>
        <input v-model="newtask" @keypress.enter="addtask" type="text" placeholder="Escibe tu tarea">
        <p class="help" v-show="newtask != ''"> Presiona enter para configurar</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}

.help {
  margin: 0;
  font-size: 10px;
  opacity: 0.9;
}

.button {
  display: inline-block;
  align-items: center;
  background-color: #fcd5ce;
  padding: 0 5px;
  border-radius: 2px;
  color: white;

}

.button:hover {
  cursor: pointer;
  background-color: orange;
}

.task {
  display: flex;
  justify-content: space-between;
  background-color: #D8E2DC;
  border-radius: 4px;
  padding: 2px 8px;
  margin-bottom: 2px;
  padding-right: 2px;
}

.subtittle {
  padding: 0;
  margin: 0;
  text-align: center;
  opacity: 0.6;
  margin-bottom: 16px;
}

h1 {
  text-transform: uppercase;
  text-align: center;
  padding: 0;
  margin: 0;
  font-size: 24px;
}

input {
  width: 100%;
  box-sizing: border-box;
  border: none;
  outline: none;
  padding: 3px 6px;
  border-radius: 4px;

}

.card {
  font-family: 'Poppins', sans-serif;
  background-color: #F8EDEB;
  max-width: 520px;
  border-radius: 8px;
  padding: 18px 16px;
  margin: 0 auto;
}

.task:hover {
  background-color: #cdb2ab;
}
</style>