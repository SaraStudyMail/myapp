<script setup>
  import { ref, onMounted } from 'vue'

  const post = ref([])
  onMounted(async () => {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts")
    post.value = await res.json()
  })
</script>

<template>
  <v-container style="max-width: 600px;" class="py-6">
    <h2 class="text-h5 font-weight-bold mb-4">List Posts</h2>

    <v-card
      v-for="list in post" :key="list.id" class="mb-4 pa-2" rounded="lg" elevation="2">
      <v-card-title class="text-wrap text-subtitle-1 font-weight-bold">
        <v-chip color="primary" variant="tonal" size="small" class="mr-2">
          #{{ list.id }}
        </v-chip>
        {{ list.title }}
      </v-card-title>
      <v-card-text class="text-medium-emphasis">
        {{ list.body }}
      </v-card-text>
    </v-card>
  </v-container>
</template>
