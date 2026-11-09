<script setup>
  import { ref } from 'vue'

  const username = ref('')
  const password = ref('')
  const loginStatus = ref(false)

  const submit = () => {
    if (username.value === 'admin' && password.value === 'admin') {
      loginStatus.value = true
      alert('Login successful')
    } else {
      loginStatus.value = false
      alert('โม้')
    }
  }

  const cancel = () => {
    username.value = ''
    password.value = ''
    loginStatus.value = false
  }
</script>

<template>
  <v-container style="max-width: 400px;">


    <h1>settawut</h1>
    <v-text-field v-model="username" label="Username" prepend-icon="mdi-account"></v-text-field>
    <v-text-field v-model="password" label="Password" prepend-icon="mdi-lock" type="password"></v-text-field>
    <div class="text-center">
      <v-btn color="green" prepend-icon="mdi-check" class="mr-2" @click="submit">Submit</v-btn>
      <v-btn color="red" prepend-icon="mdi-close" @click="cancel">Cancel</v-btn>
    </div>

    <p v-if="loginStatus">Login successful!</p>
  </v-container>
</template>
