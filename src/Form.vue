<script setup>
import {ref} from 'vue'

const money = ref(0)
const ot = ref(0)
const total = ref(0)
const tax = ref(0)

function calary(){
  tax.value = (3/100)*money.value
  total.value = (money.value+ot.value)-tax.value
}
const clearall = ()=>{
  money = 0
  ot = 0
  total = 0
}
</script>

<template>
  <h2>การใช้ form</h2>
  <input type="number" placeholder="input money" v-model="money">
  <input type="number" placeholder="input OT" v-model="ot">
  <button @click="calary">kum nuan</button>
  <button @click="clearall">clear</button>
  <p>money you: {{ money }}</p>
  <p>ot you: {{ ot }}</p>
  <p>huk na tee jai: {{ tax }}</p>
  <p>total money you: {{ total }}</p>
</template>
