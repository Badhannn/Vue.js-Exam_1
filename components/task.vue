<template>
    <div class="container mx-auto my-8">
      <ul>
        <li v-for="(task, index) in tasks" :key="index" class="mb-4">
          {{ task.name }} - {{ task.time }} minutes
          <button @click="openEditForm(index)" class="ml-2 bg-blue-500 text-white px-2 py-1 rounded">Edit</button>
        </li>
      </ul>
  
      <div v-if="isEditing" class="fixed top-0 left-0 w-full h-full bg-gray-800 bg-opacity-75 flex items-center justify-center">
        <div class="bg-white p-6 rounded shadow-lg">
          <form @submit.prevent="updateTask">
            <div class="mb-4">
              <label for="editName" class="block text-sm font-medium text-gray-600">Name:</label>
              <input v-model="editName" type="text" id="editName" class="mt-1 p-2 w-full border rounded-md" />
            </div>
  
            <div class="mb-4">
              <label for="editTime" class="block text-sm font-medium text-gray-600">Time:</label>
              <input v-model="editTime" type="number" id="editTime" class="mt-1 p-2 w-full border rounded-md" />
            </div>
  
            <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, reactive } from 'vue';
  
  const tasks = ref([
    { name: 'Task 1', time: 30 },
    { name: 'Task 2', time: 40 },
    { name: 'Task 3', time: 60 },
    { name: 'Task 4', time: 45 },
    { name: 'Task 5', time: 50 },
  ]);
  
  const isEditing = ref(false);
  const editIndex = ref(null);
  const editName = ref('');
  const editTime = ref(0);
  
  const openEditForm = (index) => {
    isEditing.value = true;
    editIndex.value = index;
    editName.value = tasks.value[index].name;
    editTime.value = tasks.value[index].time;
  };
  
  const updateTask = () => {
    tasks.value[editIndex.value].name = editName.value;
    tasks.value[editIndex.value].time = editTime.value;
  
    isEditing.value = false;
    editIndex.value = null;
    editName.value = '';
    editTime.value = 0;
  };
  </script>
  
  <style scoped>
 
  </style>
  