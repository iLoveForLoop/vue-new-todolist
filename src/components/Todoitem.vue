<script setup>
import { ref } from 'vue'

const props = defineProps({
  task: {},
  index: {}
})

const emit = defineEmits(['delete-data', 'toggle-update'])

const { index } = props

const handleDelete = () => {
  emit('delete-data', index)
}

const handleEditToggle = () => {
  emit('toggle-update', { isEdit: true, index: index })
}
</script>

<template>
  <div class="task">
    <div class="text-div">
      <p>{{ task }}</p>
    </div>

    <div class="btns">
      <div class="btn-div">
        <button @click="handleEditToggle">Edit</button>
      </div>

      <div class="btn-div">
        <button @click="handleDelete">Delete</button>
      </div>
    </div>
  </div>
</template>


<style scoped>
.task {
  display: flex;
  justify-content: space-between;
  padding: 15px;
  background-color: aliceblue;
  width: 50%;
}

p {
  display: inline-block;
}

button {
  padding: 5px 20px;
}

.btn-div {
  display: flex;
  justify-content: center;
  align-items: center;
}

.btns {
  display: flex;
  gap: 1em;
}
</style>