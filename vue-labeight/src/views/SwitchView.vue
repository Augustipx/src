<script setup lang="ts">
import { ref } from 'vue'

// 当前身份，用于动态切换用户界面
const role = ref('guest')

// v-if 与 v-show 对比用
const show = ref(true)
</script>

<template>
  <h2>三、动态切换用户界面（示例3-4：v-if / v-else-if / v-else）</h2>

  <nav>
    <button :class="{ active: role === 'guest' }" @click="role = 'guest'">未登录</button>
    <button :class="{ active: role === 'user' }" @click="role = 'user'">普通用户</button>
    <button :class="{ active: role === 'vip' }" @click="role = 'vip'">VIP会员</button>
    <button :class="{ active: role === 'admin' }" @click="role = 'admin'">管理员</button>
  </nav>

  <div class="panel">
    <template v-if="role === 'guest'">
      <h3>请先登录</h3>
      <p>当前是游客状态，登录后可以看到更多内容。</p>
    </template>
    <template v-else-if="role === 'user'">
      <h3>普通用户</h3>
      <p>你好，普通用户！你可以浏览和评论。</p>
    </template>
    <template v-else-if="role === 'vip'">
      <h3>VIP 会员</h3>
      <p>尊贵的 VIP，你可以观看高清视频并享受去广告特权。</p>
    </template>
    <template v-else>
      <h3>管理员</h3>
      <p>管理员您好，您可以进入后台管理系统。</p>
    </template>
  </div>

  <h3 class="sub">v-if 与 v-show 的区别</h3>
  <button @click="show = !show">{{ show ? '隐藏' : '显示' }}</button>
  <p v-if="show" class="line">这段文字由 v-if 控制（条件为假时不渲染，DOM 中不存在）</p>
  <p v-show="show" class="line">这段文字由 v-show 控制（用 display:none 隐藏，DOM 中一直存在）</p>
</template>

<style scoped>
nav {
  margin-bottom: 16px;
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

.panel {
  min-height: 90px;
  padding: 12px 20px;
  background: #f7f9fc;
  border-left: 4px solid #3b82f6;
  border-radius: 4px;
}

.panel h3 {
  margin: 4px 0 8px;
}

.sub {
  margin-top: 24px;
}

.line {
  margin: 8px 0;
  padding: 6px 12px;
  background: #f0f4ff;
  border-radius: 4px;
  font-size: 14px;
}
</style>
