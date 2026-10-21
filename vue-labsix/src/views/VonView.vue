<script setup lang="ts">
import { ref } from 'vue'

const counter = ref(0)
const message = ref('Hello Vue')
const htmlText = ref('<b style="color:#e23c3c">这段文字由 v-html 渲染</b>')

function add(e: MouseEvent) {
  counter.value++
  console.log(e)
}
</script>

<template>
  <h2>一、v-on 事件绑定</h2>
  <button v-on:click="counter = counter + 1">加1（内联表达式）</button>
  <button v-on:click="add">加1（调用方法）</button>
  <p>按钮单击了{{ counter }}次</p>

  <h2>v-text 与 v-html</h2>
  <p v-text="message"></p>
  <p v-text="htmlText"></p>
  <p v-html="htmlText"></p>
</template>

<style scoped>
button {
  margin-right: 8px;
  padding: 6px 16px;
  cursor: pointer;
}
</style>
