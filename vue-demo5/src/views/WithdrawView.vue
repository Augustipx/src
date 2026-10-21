<script lang="ts">
export default {
  name: 'WithdrawView',
  data() {
    return {
      balance: 1000, // 账户余额
      amount: '', // 支取金额
      message: '', // 提醒信息
      success: false,
    }
  },
  methods: {
    withdraw() {
      const money = Number(this.amount)

      if (this.amount === '' || isNaN(money) || money <= 0) {
        this.success = false
        this.message = '请输入正确的支取金额！'
      } else if (money > this.balance) {
        this.success = false
        this.message = '支取金额不能大于账户余额！'
      } else {
        this.balance = this.balance - money
        this.success = true
        this.message = '支取成功，当前账户余额为 ' + this.balance + ' 元'
      }
    },
  },
}
</script>

<template>
  <div class="card">
    <h2>简易版银行支取金额提醒</h2>

    <div class="field">
      <label>账户余额：</label>
      <span>{{ balance }} 元</span>
    </div>

    <div class="field">
      <label>支取金额：</label>
      <input v-model="amount" type="text" placeholder="请输入支取金额" />
    </div>

    <button class="submit" @click="withdraw">支取</button>

    <p v-if="message" class="tip" :class="{ ok: success }">{{ message }}</p>
  </div>
</template>
