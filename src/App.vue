<script setup>
import { ref, reactive } from 'vue'

const boolean = ref(false)

const count = ref(0)
const detail = ref({
  name: 'โต้',
  cash: 0,
})

const student = {
  name: 'แกรม',
  depart: 'ไก่',
  image: 'https://bigrat.monster/media/bigrat.jxl',
}

function auto() {
  detail.value.cash += 50
}
</script>

<template>
  <h1>boolean เป็น {{ boolean }}</h1>
  <button @click="boolean = true">เปลี่ยนเป็น true</button>
  <button @click="boolean = false">เปลี่ยนเป็น false</button>
  <button @click="boolean = !boolean">เปลี่ยน {{ boolean }} ให้เป็น {{ !boolean }}</button>
  <h1 v-if="boolean == true">เข้าสู่ระบบแล้ว</h1>
  <h1 v-if="boolean == false">ออกจากระบบแล้ว</h1>

  <div v-if="boolean == true">
    <p>{{ detail.name }}มี {{ detail.cash }} บาท</p>
    <button @click="auto()">เพิ่มจำนวน</button>
    <button @click="detail.cash -= 100">เพิ่มจำนวน</button>

    <p>จำนวน: {{ count }}</p>
    <button @click="count++">เพิ่มจำนวน</button>
    <button @click="count--">ลดจำนวน</button>

    <h1>ข้อมูลนักเรียน</h1>
    <p>ชื่อ: {{ student.name }}</p>
    <p>สาขา: {{ student.depart }}</p>
    <img :src="student.image" />
  </div>
</template>
