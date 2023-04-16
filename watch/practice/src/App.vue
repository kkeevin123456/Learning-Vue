
<template>
  <input type="text" :style="dynamicStyle" v-model="text" />
  <br /><br />
  <!-- <input type="text" v-model="text.label" /> -->
</template>

<script setup>
import { reactive, ref } from '@vue/reactivity'
import { watchEffect, watch } from '@vue/runtime-core'

// 物件
// const text = ref({
//   levels: {
//     text: "hello",
//   }, label: 'main',
// })

// 不需要加 value 就可以取道值
// 習慣: 物件用 reactive; number, boolean 用 ref;
// const text = reactive({
//   levels: {
//     text: "hello",
//   },
// })

// watch, 後面那個 function 第一個參數是當前觀察的物件變化後新的值，第二個參數是舊的值
// watch 預設是監聽第一層而已，所以物件裡面的東西會監聽不到，所以我們必須要將第三個變數裡面的 deep 打開
// 這樣才會去監聽深層的變化，又或者我們可以改變監聽的目標
// watch(text, (newData, oldData) => {
//   console.log(newData.levels.text, oldData.levels.text)
// }, { deep: true })

// watch(() => text.value.levels.text, (newData, oldData) => {
//   console.log(newData, oldData)
// })

// 一次監聽多個物件
// watch(
//   [() => text.value.levels.text, ()=> text.value.label], 
//   (newData, oldData) => {
//   console.log(newData, oldData)
// })

// watchEffect
// 會自動監聽使用到的物件，呼叫他回傳的 function 則可以停止監聽
// const stop = watchEffect(() => {
//   console.log('levels.text: ' + text.value.levels.text)
//   text.value.label = text.value.levels.text;
// })

// watch(() => text.value.label,
//  (newData, oldData) => {
//   console.log('label: ' + newData);
//   if (newData === 'stop') stop();
// })


const text = ref('hello')

const dynamicStyle = reactive({
  color: 'red',
  fontSize: '20px',
  transition: 'ease-in-out 0.2s',
})

watch(text,
  (newData, _) => {
    if (newData === 'green')
      dynamicStyle.color = 'green';
    else if (newData === 'red')
      dynamicStyle.color = 'red';
    else if (newData === 'blue')
      dynamicStyle.color = 'blue';
    
    if (newData === 'big') {
      const oldSize = dynamicStyle.fontSize.length;
      dynamicStyle.fontSize = (Number(dynamicStyle.fontSize.slice(0, oldSize-2)) + 5).toString() + 'px'
    }
    else if (newData === 'small') {
      const oldSize = dynamicStyle.fontSize.length;
      dynamicStyle.fontSize = (Number(dynamicStyle.fontSize.slice(0, oldSize-2)) - 5).toString() + 'px'
    }
  }
)

</script>

<style scoped>
</style>
