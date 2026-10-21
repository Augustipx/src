<script setup lang="ts">
import { ref } from 'vue'
import VonView from './views/VonView.vue'
import EventView from './views/EventView.vue'
import PoemView from './views/PoemView.vue'

const current = ref('von')
</script>

<template>
  <h1>实验六 Vue 的常用指令</h1>

  <nav>
    <button :class="{ active: current === 'von' }" @click="current = 'von'">1、v-on 事件绑定</button>
    <button :class="{ active: current === 'event' }" @click="current = 'event'">
      2、事件修饰符
    </button>
    <button :class="{ active: current === 'poem' }" @click="current = 'poem'">
      3、显示/隐藏诗词
    </button>
  </nav>

  <VonView v-if="current === 'von'" />
  <EventView v-else-if="current === 'event'" />
  <PoemView v-else />
</template>

<style scoped>
h1 {
  font-size: 22px;
}

nav {
  margin-bottom: 20px;
}

nav button {
  margin-right: 8px;
  padding: 6px 14px;
  border: 1px solid #ccc;
  background: #f5f5f5;
  border-radius: 4px;
  cursor: pointer;
}

nav button.active {
  background: #3b82f6;
  border-color: #3b82f6;
  color: #fff;
}
</style>
