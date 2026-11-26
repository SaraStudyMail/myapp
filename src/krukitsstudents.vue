<script setup>
import { ref, onMounted } from 'vue'

const info = ref({})
const students = ref([])
const selectedStudent = ref(null)

onMounted(async () => {
  const res = await fetch('https://ntc2.technicnan.ac.th/public/nan_api/')
  const json = await res.json()

  info.value = json
  students.value = json.data
})
</script>

<template>
  <div style="border: 1px solid black; padding: 10px; margin-bottom: 20px;">
    <h3>{{ info.title }}</h3>
    <p>ชั้น : {{ info.class }}</p>
    <p>ครูที่ปรึกษา : {{ info.teacher }}</p>
    <p>วันที่ : {{ info.date }}</p>
  </div>

  <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px;">
    <div
      v-for="student in students"
      :key="student.student_id"
      @click="selectedStudent = student"
      style="border: 1px solid black; padding: 10px; text-align: center; cursor: pointer;"
    >
      <img :src="student.image_url" width="100" />
      <p>เลขที่ {{ student.no }}</p>
      <p><b>{{ student.full_name }}</b></p>
      <p>รหัส {{ student.student_id }}</p>
      <p>( {{ student.prefix === 'นาย' ? 'ชาย' : 'หญิง' }} )</p>
    </div>
  </div>

  <div
    v-if="selectedStudent"
    style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.5); display: flex; justify-content: center; align-items: center;"
  >
    <div style="background: white; border: 1px solid black; padding: 20px; text-align: center;">
      <img :src="selectedStudent.image_url" width="120" />
      <p><b>{{ selectedStudent.full_name }}</b></p>
      <p>เลขที่ : {{ selectedStudent.no }}</p>
      <p>รหัส : {{ selectedStudent.student_id }}</p>
      <p>เพศ : {{ selectedStudent.prefix === 'นาย' ? 'ชาย' : 'หญิง' }}</p>
      <button @click="selectedStudent = null">ปิด</button>
    </div>
  </div>
</template>
