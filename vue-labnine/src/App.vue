<script setup lang="ts">
import { computed, ref } from 'vue'

interface Student {
  id: number
  name: string
  score: number
}

interface Book {
  id: number
  title: string
  author: string
  price: number
  description: string
}

interface Product {
  id: number
  name: string
  price: number
}

interface CartItem extends Product {
  quantity: number
}

const studentNames = [
  '张伟',
  '王芳',
  '李娜',
  '刘洋',
  '陈晨',
  '杨帆',
  '赵磊',
  '黄静',
  '周杰',
  '吴敏',
  '徐涛',
  '孙悦',
  '胡雪',
  '朱琳',
  '高翔',
  '林峰',
  '何雨',
  '郭佳',
  '马超',
  '罗欣',
  '梁宇',
  '宋洁',
  '郑浩',
  '谢婷',
  '韩雪',
  '唐磊',
]

function createStudents(): Student[] {
  return studentNames.map((name, index) => ({
    id: index + 1,
    name,
    score: Math.floor(Math.random() * 61) + 40,
  }))
}

const studentData = ref<Student[]>(createStudents())

function refreshScores() {
  studentData.value = createStudents()
}

function levelClass(score: number) {
  if (score >= 90) return 'excellent'
  if (score >= 80) return 'good'
  if (score >= 60) return 'pass'
  return 'fail'
}

const books: Book[] = [
  {
    id: 1,
    title: 'Vue.js 3 Web开发实战',
    author: '陈陆扬',
    price: 79,
    description: '学习 <strong>Vue 3</strong> 基础语法和组件化开发。',
  },
  {
    id: 2,
    title: 'JavaScript高级程序设计',
    author: 'Matt Frisbie',
    price: 129,
    description: '学习 JavaScript 语言核心和浏览器编程。',
  },
  {
    id: 3,
    title: 'HTML5与CSS3基础教程',
    author: 'Elizabeth Castro',
    price: 59,
    description: '学习网页的结构和样式。',
  },
  {
    id: 4,
    title: '深入浅出Node.js',
    author: '朴灵',
    price: 69,
    description: '学习 Node.js 模块和异步编程。',
  },
]

const products: Product[] = [
  { id: 1, name: '机械键盘', price: 199 },
  { id: 2, name: '无线鼠标', price: 89 },
  { id: 3, name: '降噪耳机', price: 299 },
  { id: 4, name: 'USB-C扩展坞', price: 159 },
]

const cart = ref<CartItem[]>([])

function addToCart(product: Product) {
  const item = cart.value.find((cartItem) => cartItem.id === product.id)
  if (item) {
    item.quantity++
  } else {
    cart.value.push({ ...product, quantity: 1 })
  }
}

function decreaseQuantity(item: CartItem) {
  if (item.quantity > 1) {
    item.quantity--
  }
}

function removeFromCart(id: number) {
  cart.value = cart.value.filter((item) => item.id !== id)
}

function clearCart() {
  cart.value = []
}

const totalQuantity = computed(() => cart.value.reduce((sum, item) => sum + item.quantity, 0))

const totalPrice = computed(() =>
  cart.value.reduce((sum, item) => sum + item.price * item.quantity, 0),
)
</script>

<template>
  <div class="app">
    <h1>Vue 常用指令练习</h1>
    <p class="intro">
      本页面练习 <code>v-text</code>、<code>v-html</code>、<code>v-bind</code>、
      <code>v-if</code> 和 <code>v-for</code>。
    </p>

    <section>
      <h2>1. 学生成绩表</h2>
      <p>
        <span v-text="'每次刷新页面，学生的成绩都会随机变化。'"></span>
        <button type="button" @click="refreshScores">重新生成成绩</button>
      </p>

      <table>
        <thead>
          <tr>
            <th>序号</th>
            <th>姓名</th>
            <th>成绩</th>
            <th>等级</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="student in studentData" :key="student.id">
            <td>{{ student.id }}</td>
            <td>{{ student.name }}</td>
            <td>{{ student.score }}</td>
            <td>
              <span
                class="level"
                :class="levelClass(student.score)"
                :title="`${student.name}的成绩为${student.score}分`"
              >
                <template v-if="student.score >= 90">优秀</template>
                <template v-else-if="student.score >= 80">良好</template>
                <template v-else-if="student.score >= 60">及格</template>
                <template v-else>不及格</template>
              </span>
            </td>
          </tr>
        </tbody>
      </table>
    </section>

    <section>
      <h2>2. 书籍列表</h2>
      <p>共 <span v-text="books.length"></span> 本书。使用 <code>v-for</code> 循环显示。</p>

      <ul class="book-list">
        <li v-for="(book, index) in books" :key="book.id">
          <h3>{{ index + 1 }}. {{ book.title }}</h3>
          <p>作者：{{ book.author }}</p>
          <p v-html="book.description"></p>
          <strong>价格：¥{{ book.price }}</strong>
        </li>
      </ul>
    </section>

    <section>
      <h2>3. 简易购物车</h2>

      <h3>商品列表</h3>
      <ul class="product-list">
        <li v-for="product in products" :key="product.id">
          <span>{{ product.name }}，价格 ¥{{ product.price }}</span>
          <button type="button" @click="addToCart(product)">加入购物车</button>
        </li>
      </ul>

      <h3>购物车（{{ totalQuantity }} 件）</h3>
      <p v-if="cart.length === 0">购物车为空，请先选择商品。</p>
      <ul v-else class="cart-list">
        <li v-for="item in cart" :key="item.id">
          <span class="item-name">{{ item.name }}</span>
          <span>单价：¥{{ item.price }}</span>
          <button type="button" :disabled="item.quantity <= 1" @click="decreaseQuantity(item)">
            -
          </button>
          <span>数量：{{ item.quantity }}</span>
          <button type="button" @click="addToCart(item)">+</button>
          <button type="button" @click="removeFromCart(item.id)">删除</button>
        </li>
      </ul>

      <p class="total">
        合计：<strong>¥{{ totalPrice }}</strong>
      </p>
      <button v-if="cart.length" type="button" @click="clearCart">清空购物车</button>
    </section>
  </div>
</template>

<style scoped>
:global(body) {
  margin: 0;
  color: #333;
  background: #f5f5f5;
  font-family: 'Microsoft YaHei', Arial, sans-serif;
}

.app {
  max-width: 960px;
  margin: 20px auto;
  padding: 20px;
  background: #fff;
  border: 1px solid #ddd;
}

h1 {
  margin-top: 0;
  text-align: center;
}

.intro {
  color: #666;
  text-align: center;
}

h2 {
  margin-top: 30px;
  padding-bottom: 8px;
  border-bottom: 1px solid #ddd;
  font-size: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 6px;
  border: 1px solid #ccc;
  text-align: left;
}

th {
  background: #eee;
}

button {
  margin-left: 6px;
  padding: 4px 9px;
  border: 1px solid #999;
  background: #f8f8f8;
  cursor: pointer;
}

button:disabled {
  color: #aaa;
  cursor: not-allowed;
}

.level {
  padding: 2px 6px;
  border: 1px solid #ccc;
}

.excellent {
  color: green;
  background: #f0fff0;
}

.good {
  color: #0055aa;
  background: #eef5ff;
}

.pass {
  color: #996600;
  background: #fffbe6;
}

.fail {
  color: red;
  background: #fff0f0;
}

.book-list,
.product-list,
.cart-list {
  padding-left: 20px;
}

.book-list li,
.product-list li,
.cart-list li {
  margin-bottom: 10px;
}

.book-list h3 {
  margin: 0 0 5px;
  font-size: 16px;
}

.book-list p {
  margin: 4px 0;
}

.cart-list li {
  padding: 8px;
  border: 1px solid #ddd;
  list-style: none;
}

.item-name {
  display: inline-block;
  min-width: 100px;
}

.total {
  font-size: 18px;
}
</style>
