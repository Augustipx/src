<script setup lang="ts">
import { ref } from 'vue'
import ProfileView from './views/ProfileView.vue'
import ModelView from './views/ModelView.vue'
import SwitchView from './views/SwitchView.vue'

const current = ref('profile')
</script>

<template>
  <h1>实验八 Vue 的常用指令</h1>

  <nav>
    <button :class="{ active: current === 'profile' }" @click="current = 'profile'">
      1、个人简介（v-model）
    </button>
    <button :class="{ active: current === 'model' }" @click="current = 'model'">
      2、v-model 修饰符
    </button>
    <button :class="{ active: current === 'switch' }" @click="current = 'switch'">
      3、动态切换用户界面（v-if）
    </button>
  </nav>

  <ProfileView v-if="current === 'profile'" />
  <ModelView v-else-if="current === 'model'" />
  <SwitchView v-else />
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
