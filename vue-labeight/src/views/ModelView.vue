<script setup lang="ts">
import { computed, ref } from 'vue'

// v-model.lazy：只在失去焦点或回车时才更新绑定值
const lazyMsg = ref('')
const lazyLive = ref('')

// v-model.number：把输入自动转换为数字类型
const age = ref(18)
const ageType = computed(() => typeof age.value)

// v-model.trim：自动去掉首尾空格
const name = ref('')
</script>

<template>
  <h2>二、v-model 修饰符</h2>

  <section class="box">
    <h3>1、.lazy 懒加载</h3>
    <input
      v-model.lazy="lazyMsg"
      type="text"
      placeholder="输入后按回车或点走鼠标"
      @input="lazyLive = ($event.target as HTMLInputElement).value"
    />
    <p>实时输入（@input）：{{ lazyLive }}</p>
    <p>绑定值（失焦 / 回车后才更新）：{{ lazyMsg }}</p>
  </section>

  <section class="box">
    <h3>2、.number 转数字</h3>
    <input v-model.number="age" type="number" />
    <p>age = {{ age }}（类型：{{ ageType }}）</p>
    <p>age + 1 = {{ age + 1 }}</p>
  </section>

  <section class="box">
    <h3>3、.trim 去首尾空格</h3>
    <input v-model.trim="name" type="text" placeholder="试试输入前后带空格的文字" />
    <p>绑定值："{{ name }}"</p>
    <p>字符个数：{{ name.length }}</p>
  </section>

  <p class="tip">修饰符让 v-model 在同步数据时做一些额外处理：.lazy 延迟同步，.number 转成数字，.trim 去掉首尾空格。</p>
</template>

<style scoped>
.box {
  margin-bottom: 18px;
  padding: 10px 18px;
  background: #f7f9fc;
  border-left: 4px solid #3b82f6;
  border-radius: 4px;
}

.box h3 {
  margin: 6px 0 10px;
  font-size: 16px;
}

input {
  padding: 6px 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
  min-width: 220px;
}

p {
  margin: 6px 0;
}

.tip {
  color: #888;
  font-size: 14px;
}
</style>
