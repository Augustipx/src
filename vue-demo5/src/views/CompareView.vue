<script lang="ts">
export default {
  name: 'CompareView',
  data() {
    return {
      num1: '', // 第一个数
      num2: '', // 第二个数
      result: '', // 比较结果
    }
  },
  methods: {
    compare() {
      const a = Number(this.num1)
      const b = Number(this.num2)

      if (this.num1 === '' || this.num2 === '' || isNaN(a) || isNaN(b)) {
        this.result = '请输入两个数字！'
      } else if (a > b) {
        this.result = a + ' 大于 ' + b
      } else if (a < b) {
        this.result = a + ' 小于 ' + b
      } else {
        this.result = a + ' 等于 ' + b
      }
    },
  },
}
</script>

<template>
  <div class="card">
    <h2>两个数大小比较</h2>

    <div class="field">
      <label>第一个数：</label>
      <input v-model="num1" type="text" placeholder="请输入第一个数" />
    </div>

    <div class="field">
      <label>第二个数：</label>
      <input v-model="num2" type="text" placeholder="请输入第二个数" />
    </div>

    <button class="submit" @click="compare">比较</button>

    <p v-if="result" class="tip ok">{{ result }}</p>
  </div>
</template>
