<script setup>
import { ref, watch } from 'vue'

const data_list = ref(JSON.parse(localStorage.getItem('data_list') || '[]'))
const title = ref('')
const amount = ref('')
const editIndex = ref(-1)
const editType = ref('income')
const error = ref('')

watch(data_list, () => {
  localStorage.setItem('data_list', JSON.stringify(data_list.value))
}, { deep: true })

function add(type) {
  if (title.value.trim() == '' || amount.value == '' || Number(amount.value) <= 0) {
    error.value = 'กรุณากรอกรายการและจำนวนเงินให้ครบถ้วนและถูกต้อง'
    return
  }
  data_list.value.push({ title: title.value.trim(), amount: Number(amount.value), type: type })
  title.value = ''
  amount.value = ''
  error.value = ''
}

function edit(index) {
  editIndex.value = index
  title.value = data_list.value[index].title
  amount.value = data_list.value[index].amount
  editType.value = data_list.value[index].type
  error.value = ''
}

function save() {
  if (title.value.trim() == '' || amount.value == '' || Number(amount.value) <= 0) {
    error.value = 'กรุณากรอกรายการและจำนวนเงินให้ครบถ้วนและถูกต้อง'
    return
  }
  data_list.value[editIndex.value].title = title.value.trim()
  data_list.value[editIndex.value].amount = Number(amount.value)
  data_list.value[editIndex.value].type = editType.value
  cancelEdit()
}

function cancelEdit() {
  editIndex.value = -1
  title.value = ''
  amount.value = ''
  error.value = ''
}

function remove(index) {
  data_list.value.splice(index, 1)
  if (editIndex.value == index) {
    cancelEdit()
  } else if (editIndex.value > index) {
    editIndex.value--
  }
}

function getBalance() {
  let total = 0
  for (const item of data_list.value) {
    if (item.type == 'income') {
      total += item.amount
    } else {
      total -= item.amount
    }
  }
  return total
}
</script>

<template>
  <v-container style="max-width: 500px;" class="text-center">
    <h1>รายรับ-รายจ่าย</h1>
    <h2 :class="getBalance() >= 0 ? 'text-green' : 'text-red'" class="mb-4">
      คงเหลือ {{ getBalance() }} บาท
    </h2>

    <v-alert v-if="error" type="error" density="compact" class="mb-3">
      {{ error }}
    </v-alert>

    <v-text-field v-model="title" label="รายการ" @input="error = ''" />
    <v-text-field v-model="amount" label="จำนวนเงิน" type="number" @input="error = ''" />

    <v-radio-group v-if="editIndex != -1" v-model="editType" inline hide-details class="d-flex justify-center mb-2">
      <v-radio label="รายรับ" value="income" color="green" />
      <v-radio label="รายจ่าย" value="expense" color="red" />
    </v-radio-group>

    <div v-if="editIndex == -1">
      <v-btn color="green" class="mr-2" @click="add('income')">+ รายรับ</v-btn>
      <v-btn color="red" @click="add('expense')">- รายจ่าย</v-btn>
    </div>
    <div v-else>
      <v-btn color="blue" class="mr-2" @click="save">บันทึก</v-btn>
      <v-btn color="grey" @click="cancelEdit">ยกเลิก</v-btn>
    </div>

    <br>
    <v-list>
      <v-list-item
        v-for="(item, index) in data_list"
        :key="index"
        :class="{ 'bg-grey-lighten-3': editIndex == index }"
      >
        <div class="d-flex align-center">
          <span>{{ item.title }}</span>
          <v-spacer />
          <span :class="item.type == 'income' ? 'text-green' : 'text-red'" class="mr-2">
            {{ item.type == 'income' ? '+' : '-' }}{{ item.amount }}
          </span>
          <v-btn size="small" color="orange" class="mr-2" @click="edit(index)">แก้ไข</v-btn>
          <v-btn size="small" color="red" @click="remove(index)">ลบ</v-btn>
        </div>
      </v-list-item>
    </v-list>
  </v-container>
</template>
