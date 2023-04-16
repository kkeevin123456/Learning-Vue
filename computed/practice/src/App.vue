
<template>
  <h1>Computed 計算屬性</h1>
  
  <input type="text" v-model="text" />
  <br /><br />
  <input type="number" v-model="num" />

  <h3>{{ numFormat }}</h3>
</template>

<script setup>
import { computed, ref } from '@vue/reactivity';


const num = ref(0.5);
const text = ref('Hello World!');

// computed 裡面吃一個 function 
// 回傳一個響應式的物件，就不是一個 function 了，所以 numFormat 會變成一個物件
// 跟用 function 寫最大的不同在於，只有他這個物件被改變才會計算，function 是畫面有更動都會重複計算
const numFormat = computed(() => {
  console.log('change')
  if (Number.isNaN(num.value * 100)) return num.value;
  else return (num.value*100).toString() + '%';
})

// const numFormat = () => {
//   if (Number.isNaN(num * 100)) return num;
//   else return (num*100).toString() + '%';
// }
</script>

<style scoped>
</style>
