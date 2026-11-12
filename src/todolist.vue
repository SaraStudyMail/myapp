<script setup>
  import { ref } from 'vue'

  const newTask = ref('')
  const tasks = ref([])
  const alertStatus = ref(false)

  const addTask = () => {
    if (newTask.value.trim() !== '') {
      tasks.value.push(newTask.value)
      newTask.value = ''
    }else{
      alertStatus.value = true
      setTimeout(() => {
        alertStatus.value = false
      }, 3000)
    }
  }

  const taskCount = () => {
    return tasks.value.length
  }

  const clearTasks = () => {
    tasks.value = []
  }

  const removeTask = (index) => {
    tasks.value.splice(index, 1)
  }
</script>

<template>
  <v-container style="max-width: 500px;">
    <h1 class="text-center">Todo List</h1>

    <v-text-field v-model="newTask" label="New Task" prepend-icon="mdi-plus"></v-text-field>

    <div class="text-center">
      <v-btn color="blue" prepend-icon="mdi-plus" class="mr-2" @click="addTask">Add Task</v-btn>
      <v-btn color="red" prepend-icon="mdi-delete" @click="clearTasks">Clear All</v-btn>
      <h3>Task total: {{ taskCount() }}</h3>
      <v-alert v-if="alertStatus" type="error" dismissible>Please enter a task before adding.</v-alert>
    </div>
  </v-container>

  <v-container style="max-width: 700px;">
    <table boarder="1" class="table table-striped" style="width: 100%;">
      <thead>
        <tr>
          <th class="text-left" width="80%">Task</th>
          <th class="text-left" width="20%">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task }}</td>
          <td>
            <v-btn color="red" @click="removeTask(index)">Remove</v-btn>
          </td>
        </tr>
        <tr v-if="tasks.length === 0">
          <td colspan="2" class="text-center">No tasks available.</td>
        </tr>
      </tbody>
    </table>
  </v-container>
</template>
