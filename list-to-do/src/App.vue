<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center p-4">
    <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-md">
      <h1 class="text-2xl font-bold mb-4 text-center">Fandy To Do List</h1>
      <div class="flex mb-4">
        <input type="text" v-model="state.newTask" @keyup.enter="addTask" placeholder="Tambah tugas baru..."
          class="flex-grow p-2 border rounded-l-lg focus:outline-none" />
        <button @click="addTask" class="bg-blue-500 hover:bg-blue-600 text-white px-4 rounded-r-lg">Tambah</button>
      </div>

      <ul>
        <li v-for="(task, index) in state.tasks" :key="index"
          class="flex items-center justify-between bg-gray-100 p-2 mb-2 rounded">
          <div @click="toggleTask(index)" :class="{ 'line-through text-gray-500': task.completed }"
            class="cursor-pointer flex-grow">
            {{ task.text }}
          </div>
          <button @click="deleteTask(index)"
            class="bg-red-500 hover:bg-red-600 text-white px-2 py-1 rounded text-sm">Hapus</button>
        </li>
      </ul>

      <p v-if="state.tasks.length === 0" class="text-center text-gray-500 mt-4">
        Belum ada aktivitas. Tambahkan aktivitas baru!
      </p>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const state = reactive({
  newTask: "",
  tasks: []
})

const addTask = () => {
  if (state.newTask.trim() !== "") {
    state.tasks.push({ text: state.newTask, completed: false })
    state.newTask = ""
  }
}

const deleteTask = (index) => {
  state.tasks.splice(index, 1)
}

const toggleTask = (index) => {
  state.tasks[index].completed = !state.tasks[index].completed
}
</script>

<style scoped></style>