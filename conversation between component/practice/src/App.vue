<template>
  <input type="text" v-model="msg" />
  <br />
  <!-- 將 msg v-bind 到 dataa -->
  <Child :data="msg" v-on:update="updateHandler" />
</template>

<script setup>
  import { ref } from 'vue';
  import Child from './components/Child.vue'
  let msg = ref('')

  const updateHandler = (dataFromChild) => {
    console.log(dataFromChild)
  }

</script>

<style scoped>

</style>
