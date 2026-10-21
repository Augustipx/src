<script setup lang="ts">
import { onUnmounted, ref } from 'vue'

// 一、v-bind 动态绑定 img 的 src 属性，图片 3 秒后自动改变
const IMG1 = '/img1.svg'
const IMG2 = '/img2.svg'
const src = ref(IMG1)
let timer: number | undefined

function changeSrc() {
  src.value = src.value === IMG1 ? IMG2 : IMG1
}

// 重新计时：3 秒后调用 changeSrc
function restart() {
  src.value = IMG1
  window.clearTimeout(timer)
  timer = window.setTimeout(changeSrc, 3000)
}

restart()
onUnmounted(() => window.clearTimeout(timer))

// 二、v-bind 动态切换图片的边框样式
const normal = ref(true)
const borderStyle = ref('solid')
const borderColor = ref('#3b82f6')

function toggleBorder() {
  normal.value = !normal.value
  borderStyle.value = normal.value ? 'solid' : 'dashed'
  borderColor.value = normal.value ? '#3b82f6' : '#e23c3c'
}
</script>

<template>
  <h1>实验七 v-bind 指令的使用</h1>

  <h2>一、v-bind 动态绑定 img 标签的 src 属性</h2>
  <p>当前图片地址：{{ src }}</p>
  <img :src="src" alt="示例图片" width="240" height="160" />
  <p class="tip">打开页面 3 秒后，图片的 src 自动由 img1.svg 变为 img2.svg（setTimeout 实现）。</p>
  <button @click="restart">重新计时</button>

  <h2>二、v-bind 动态切换图片边框样式</h2>
  <img
    :src="src"
    alt="示例图片"
    width="240"
    height="160"
    :style="{ borderStyle, borderColor, borderWidth: '6px' }"
  />
  <p>当前边框样式：{{ borderStyle }} / {{ borderColor }}</p>
  <button @click="toggleBorder">切换边框样式</button>
</template>

<style scoped>
h1 {
  font-size: 22px;
}

h2 {
  font-size: 17px;
}

img {
  display: block;
  margin: 10px 0;
}

button {
  padding: 6px 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background: #f5f5f5;
  cursor: pointer;
}

.tip {
  color: #888;
  font-size: 14px;
}
</style>
