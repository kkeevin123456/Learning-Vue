
<template>
  <p v-for="item in dataList">
    {{ item }}
  </p>

  <!-- 注意: 這邊跟 py 不同的是 value 會在前面 -->
  <p v-for="(v, k, index) in dataDict"> 
    <span class="hint" v-if="index !== 2">
      {{index}}. {{ k }}: {{ v }}
    </span>
  </p>

  <!-- key 可以去綁定一個值，當這個值有變化的時候，會重新渲染該 class -->
  <p class="test-cls" :key="test">
    {{ test }}
  </p>

  <!-- 效果跟上面的一樣 -->
  <!-- <p class="test-cls" v-if="test === 'first'">
    {{ test }}
  </p>

  <p class="test-cls" v-else-if="test === 'second'">
    {{ test }}
  </p> -->
</template>

<script setup>
import { ref } from 'vue';
const test = ref('first')

const dataList = [
  'a',
  'b',
  'c',
  'd',
]
const dataDict = {
  'a': 1,
  'b': 2,
  'c': 3,
  'd': 4,
}

setTimeout(() => {
  test.value = 'second'
}, 2000)
</script>

<style>
.test-cls {
  font-size: 40px;
  animation: openIn 1s ease-in-out;
}

@keyframes openIn {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
