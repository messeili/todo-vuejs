<template>
<h1>Todo App</h1>
<form @submit.prevent="addNewTodo">
  <label for="name">New Task</label>
  <input v-model="newTodo" type="text" name="todo" required>
  <button>Add new Task</button>
</form>
  <button @click="markAllDone">Mark All As Done</button>
  <button @click="deleteAll">Delete all</button>
<ul>
<li v-for="task in tasks" :key="task.id">
<h3 :class="{done:task.done}" @click="toggleDone(task)">{{task.content}}</h3>
</li>
</ul>
</template>

<script>
import {ref} from 'vue'
export default {
setup(){
  const newTodo = ref('')
  const tasks = ref([])
const addNewTodo = ()=>{
  if(newTodo.value){
    tasks.value.push({
      id: Date.now(),
      done:false,
      content: newTodo.value
    });
  }
    newTodo.value=''
}

const toggleDone = (task)=>{
  task.done = !task.done
}
const markAllDone=()=>{
tasks.value.forEach(item=>{
item.done=true
})
}
const deleteAll = ()=>{
  tasks.value.length=0
}
return{addNewTodo,newTodo,tasks,toggleDone,markAllDone,deleteAll}
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done{
  text-decoration: line-through;
}
</style>
