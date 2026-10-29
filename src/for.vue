<script setup>
import {ref} from 'vue'

const students = ref([
  {id: 1, name: "โต้", score: 50},
  {id: 2, name: "ตี๋", score: 50},
  {id: 3, name: "ฟิล์ม", score: 10},
])
</script>

<template>
  <h2>รายชื่อนักเรียน</h2>

  <ul>
    <li v-for="list in students">
        {{ list.name }} | ได้คะแนน {{ list.score }} คะแนน
    </li>
  </ul>
</template>
