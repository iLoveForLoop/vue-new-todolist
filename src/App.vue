<script setup>
import Todolist from './components/Todolist.vue'
import { ref } from 'vue'

let todoText = ref('')
const taskList = ref([])

const handleSubmit = () => {
  if (todoText.value.trim() !== '') {
    taskList.value.push(todoText.value)
    todoText.value = ''
  }
}

const handleDelete = (data) => {
  console.log('received')
  taskList.value.splice(data, 1)
}

const handleEdit = ({ index, newTask }) => {
  taskList.value[index] = newTask
}
</script>

<template>
  <h1>To Do List</h1>
  <form @submit.prevent="handleSubmit">
    <input type="text" v-model="todoText" placeholder="Enter task" @keydown.enter="handleSubmit" />
    <button type="submit">Add</button>
  </form>
  <Todolist :taskList="taskList" @edit-data="handleEdit" @delete-data="handleDelete" />
</template>

<style scoped>
h1 {
  margin: 0;
}

input {
  margin: 10px 10px;
  padding: 10px 15px;
  font-size: 18px;
}

button {
  padding: 5px 20px;
}

form {
  padding: 10px;
}
</style>
