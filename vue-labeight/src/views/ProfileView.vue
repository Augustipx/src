<script setup lang="ts">
import { reactive } from 'vue'

// v-model 双向绑定：表单数据与页面内容实时同步
const profile = reactive({
  name: '张三',
  gender: '男',
  age: 20,
  city: '北京',
  employed: false,
  intro: '大家好，我是一名 Vue 爱好者。',
})
</script>

<template>
  <h2>一、个人简介（示例3-3：v-model 双向数据绑定）</h2>

  <div class="wrap">
    <form class="form" @submit.prevent>
      <label class="row">
        <span>姓名：</span>
        <input v-model="profile.name" type="text" />
      </label>

      <label class="row">
        <span>性别：</span>
        <span class="inline">
          <label><input v-model="profile.gender" type="radio" value="男" /> 男</label>
          <label><input v-model="profile.gender" type="radio" value="女" /> 女</label>
        </span>
      </label>

      <label class="row">
        <span>年龄：</span>
        <input v-model.number="profile.age" type="number" />
      </label>

      <label class="row">
        <span>城市：</span>
        <select v-model="profile.city">
          <option value="北京">北京</option>
          <option value="上海">上海</option>
          <option value="广州">广州</option>
          <option value="深圳">深圳</option>
        </select>
      </label>

      <label class="row">
        <span>是否在职：</span>
        <input v-model="profile.employed" type="checkbox" />
      </label>

      <label class="row">
        <span>个人简介：</span>
        <textarea v-model="profile.intro" rows="3"></textarea>
      </label>
    </form>

    <div class="card">
      <h3>预览（实时更新）</h3>
      <p><span>姓名</span>{{ profile.name }}</p>
      <p><span>性别</span>{{ profile.gender }}</p>
      <p><span>年龄</span>{{ profile.age }}</p>
      <p><span>城市</span>{{ profile.city }}</p>
      <p><span>在职</span>{{ profile.employed ? '是' : '否' }}</p>
      <p><span>简介</span>{{ profile.intro }}</p>
    </div>
  </div>

  <p class="tip">修改左边表单，右边内容会立即同步变化，这就是 v-model 的双向数据绑定。</p>
</template>

<style scoped>
.wrap {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
}

.form {
  flex: 1 1 320px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.row {
  display: flex;
  align-items: center;
}

.row > span:first-child {
  width: 80px;
  flex: none;
}

input[type='text'],
input[type='number'],
select,
textarea {
  padding: 6px 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
  min-width: 180px;
}

.inline {
  display: flex;
  gap: 16px;
}

.inline label {
  display: flex;
  align-items: center;
  gap: 4px;
}

.card {
  flex: 1 1 260px;
  padding: 12px 20px;
  background: #f7f9fc;
  border-left: 4px solid #3b82f6;
  border-radius: 4px;
}

.card h3 {
  margin: 4px 0 12px;
}

.card p {
  margin: 6px 0;
}

.card span {
  display: inline-block;
  width: 52px;
  color: #888;
}

.tip {
  margin-top: 20px;
  color: #888;
  font-size: 14px;
}
</style>
