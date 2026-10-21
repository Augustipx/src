<script setup lang="ts">
import { ref } from 'vue'

const show = ref(true)
</script>

<template>
  <h2>三、显示/隐藏诗词（示例3-1）</h2>
  <button @click="show = !show">{{ show ? '隐藏诗词' : '显示诗词' }}</button>

  <div v-show="show" class="poem">
    <h3>静夜思</h3>
    <p>床前明月光，疑是地上霜。</p>
    <p>举头望明月，低头思故乡。</p>
  </div>
</template>

<style scoped>
button {
  padding: 6px 16px;
  cursor: pointer;
}

.poem {
  display: inline-block;
  margin-top: 16px;
  padding: 12px 24px;
  background: #f7f7f7;
  border-left: 4px solid #3b82f6;
  text-align: center;
}

.poem h3 {
  margin: 0 0 8px;
}

.poem p {
  margin: 4px 0;
}
</style>
