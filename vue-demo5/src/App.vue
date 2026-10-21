<script lang="ts">
import WithdrawView from './views/WithdrawView.vue'
import CompareView from './views/CompareView.vue'

export default {
  name: 'App',
  components: { WithdrawView, CompareView },
  data() {
    return {
      current: 'withdraw',
    }
  },
}
</script>

<template>
  <h1>实验五 实战练习</h1>

  <nav>
    <button :class="{ active: current === 'withdraw' }" @click="current = 'withdraw'">
      1、银行支取金额提醒
    </button>
    <button :class="{ active: current === 'compare' }" @click="current = 'compare'">
      2、两个数大小比较
    </button>
  </nav>

  <WithdrawView v-if="current === 'withdraw'" />
  <CompareView v-else />
</template>
