<script setup>
  import { ref } from 'vue';

  let newTask = ref('')
  let taskList = ref([
  {text: 'Estudiar', done: false}, 
  {text: 'Jugar Play', done: true}])

  function addTask() {
    if (newTask.value.trim()==='') return 
    taskList.value.push(
    {
      text:newTask.value,
      done:false
    
    })
    newTask.value='';
  }

  function setDone(index) {

    taskList.value[index].done = !taskList.value[index].done
    
  }

  function deleteTask(index) {
    taskList.value.splice(index,1)
  }


</script>

<template>
  <div class="card">
    <h1>Lista de cosas</h1>
    <p class="subtitle">{{ newTask }}</p>
    <div>
      <div v-for="(task, index) in taskList" :key="index" class="task" :class="{done: task.done}">{{ task.text }}<span class="button" @dblclick="deleteTask(index)" @click="setDone(index)">x</span></div>
    </div>
    <div>
      <input v-model="newTask" @keypress.enter="addTask" type="text" placeholder="Escribe tu tarea">
      <p class="help" v-show="newTask != ''">Presiona ENTER para confirmar</p>
    </div>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
  background-color: #004E89 !important;
  color: aliceblue !important;
}
.help{
  margin: 0;
  font-size: 12px;
  opacity: 0.4;
}
input{
  width: 100%;
  box-sizing: border-box;
  border: none;
  outline: none;
  padding: 3px 6px;
  border-radius: 4px;
}
.button{
  background-color: #1A659E;
  padding: 0 5px;
  border-radius: 4px;
  color: aliceblue;
  display: inline-flex;
  align-items: center;
}

.button:hover{
  cursor: pointer;
  background-color: red;
}
.task{
  background-color: #F7C59F;
  border-radius: 4px;
  padding: 2px 8px;
  padding-right: 2px;
  margin-bottom: 6px;
  display: flex;
  justify-content: space-between;
}

.task:hover{
  background-color: #FF6B35;
}
.subtitle{
  padding: 0;
  margin: 0;
  text-align: center;
  opacity: 0.6;
  margin-bottom: 16px;
}

h1{
  font-family: Agbalumo;
  text-transform: uppercase;
  text-align: center;
  padding: 0;
  margin: 0;
  font-size: 24px;
}

.card{
  background-color: #EFEFD0;
  max-width: 520px;
  border-radius: 8px;
  padding: 18px 16px;
  margin: 0 auto;
}
</style>
