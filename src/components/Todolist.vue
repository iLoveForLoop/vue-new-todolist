<script setup>
import { ref } from 'vue'
import Todoitem from './Todoitem.vue'
import Editpage from './Editpage.vue'

const emit = defineEmits(['delete-data', 'edit-data'])
const props = defineProps({
  taskList: {}
})

const { taskList } = props

let currentIndex = ref(0)
let isShow = ref(false)

const handleEdit = (newTask) => {
  console.log(newTask)
  console.log(currentIndex)
  if (newTask.trim() !== '') {
    console.log('tried to edit')
    emit('edit-data', { index: currentIndex.value, newTask: newTask })
    isShow.value = false
    console.log('i reached the buttom')
  }
}

const handleToggle = ({ isEdit, index }) => {
  isShow.value = isEdit
  currentIndex.value = index
}

const handleDelete = (data) => {
  emit('delete-data', data)
}
</script>

<template>
  <Editpage @toggle-edit="handleToggle" @edit-data="handleEdit" v-if="isShow" />

  <Todoitem
    v-for="(task, index) in taskList"
    :key="index"
    :task="task"
    :index="index"
    @delete-data="handleDelete"
    @toggle-update="handleToggle"
  />
</template>

<style scoped>
</style>