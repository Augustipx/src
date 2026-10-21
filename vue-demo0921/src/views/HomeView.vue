<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  // 1. data：组件的响应式状态，必须是个函数，返回一个对象
  data() {
    return {
      price: 10, // 单价
      count: 1, // 数量
      logs: [] as string[], // 操作日志
    }
  },

  // 2. computed：由 data 算出来的值。依赖变了会自动重算，且有缓存
  computed: {
    total(): number {
      return this.price * this.count
    },
  },

  // 3. methods：放事件处理函数和业务逻辑
  methods: {
    add(): void {
      this.count++
    },
    sub(): void {
      if (this.count > 1) this.count--
    },
    reset(): void {
      this.count = 1
      this.logs = []
    },
  },

  // 4. watch：监听某个数据的变化，去做副作用（这里记录日志）
  watch: {
    count(newVal: number, oldVal: number): void {
      this.logs.push(`数量：${oldVal} → ${newVal}`)
    },
  },
})
</script>

<template>
  <main>
    <h1>实验三：data / methods / computed / watch</h1>

    <p>单价：{{ price }} 元</p>

    <p>
      数量：
      <button @click="sub">-</button>
      <span class="count">{{ count }}</span>
      <button @click="add">+</button>
    </p>

    <p>总价：{{ total }} 元</p>

    <hr />

    <h2>操作日志（由 watch 记录）</h2>
    <p v-if="logs.length === 0">暂无</p>
    <ul>
      <li v-for="(item, index) in logs" :key="index">{{ item }}</li>
    </ul>

    <button @click="reset">重置</button>
  </main>
</template>

<style scoped>
main {
  max-width: 480px;
}

h2 {
  font-size: 1rem;
  margin-bottom: 0.5rem;
}

button {
  padding: 2px 10px;
  cursor: pointer;
}

.count {
  display: inline-block;
  min-width: 2rem;
  text-align: center;
  font-weight: bold;
}

ul {
  padding-left: 1.2rem;
  margin-bottom: 1rem;
}
</style>
