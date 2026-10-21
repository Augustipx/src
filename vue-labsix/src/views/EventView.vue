<script setup lang="ts">
function func() {
  alert('百度！')
}
</script>

<template>
  <h2>二、事件修饰符</h2>
  <p>
    <a href="http://www.baidu.com" @click="func">能访问百度</a>
  </p>
  <p>
    <a href="http://www.baidu.com" @click.prevent="func">不能访问百度（.prevent）</a>
  </p>
  <p>
    <a href="http://www.baidu.com" @click.prevent.once="func">
      第一次不能访问百度（.prevent.once）
    </a>
  </p>
  <p class="tip">提示：点击第一个链接会跳转，第二个始终不跳转，第三个只在第一次点击时不跳转。</p>
</template>

<style scoped>
p {
  line-height: 2;
}

a {
  color: #3b82f6;
}

.tip {
  margin-top: 16px;
  color: #888;
  font-size: 14px;
}
</style>
