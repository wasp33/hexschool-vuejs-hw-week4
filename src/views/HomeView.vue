<script setup>
import { ref } from 'vue'
import OnsellProduct from '@/components/OnsellProduct.vue'
import ShoppingCart from '@/components/ShoppingCart.vue'
import { toast } from 'vue3-toastify'
import 'vue3-toastify/dist/index.css'

const products = ref([
  {
    id: 1,
    name: '耳罩式藍牙耳機',
    price: 2490,
    image:
      'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    description: '舒適配戴，支援降噪技術',
  },
  {
    id: 2,
    name: '粉色耳罩式藍牙耳機',
    price: 1230,
    image:
      'https://plus.unsplash.com/premium_photo-1679913792906-13ccc5c84d44?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    description: '舒適配戴，支援降噪技術',
  },
  {
    id: 3,
    name: '耳塞型藍牙耳機',
    price: 4230,
    image:
      'https://images.unsplash.com/photo-1645845925550-639df814f0f0?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    description: '舒適配戴，支援降噪技術',
  },
])
const shopCarts = ref([])

const addToCart = (product) => {
  console.log('out =>', product)
  showSuccessToast('加入購物車成功')
  shopCarts.value.push(product)
}
const removeFromCart = (product) => {
  console.log('移除購物車')
  showSuccessToast('移除購物車成功')
  shopCarts.value = shopCarts.value.filter((item) => item.id !== product.id)
}

const showSuccessToast = (successMsg) => {
  toast.success(successMsg, {
    position: 'top-right', // Optional: customize position
  })
}
</script>

<template>
  <div id="app" class="container py-4">
    <div class="products row">
      <!-- 商品列表區 -->
      <div class="contain col-md-8">
        <h2 class="mb-3">商品列表</h2>
        <div class="row">
          <div class="col-md-4 mb-4">
            <OnsellProduct
              v-for="product in products"
              :key="product.id"
              :id="product.id"
              :name="product.name"
              :price="product.price"
              :image="product.image"
              :description="product.description"
              @emitAddToCart="addToCart"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="shopping-cart">
      <!-- 購物車區 -->
      <div>
        <h2>購物車</h2>
        <div>
          <ShoppingCart
            v-for="item in shopCarts"
            :key="item.id"
            :id="item.id"
            :name="item.name"
            :price="item.price"
            :quantity="item.quantity"
            @emitRemoveFromCart="removeFromCart"
          />
        </div>
      </div>
    </div>
    <div class="information">
      <!-- 通知元件 -->
      <div class="position-fixed top-0 end-0 p-3" style="z-index: 1050">
        <div class="toast show align-items-center text-white bg-success border-0">
          <div class="d-flex">
            <div class="toast-body">這是通知訊息</div>
            <button type="button" class="btn-close btn-close-white me-2 m-auto"></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  background: #f2f2f2f2;
}

.shopping-cart .information {
  width: 300px;
  height: 400px;
}
.container {
  background: #fff;
  float: left;
}
.content {
  display: flex;
}
.card-img-top {
  height: 150px;
  object-fit: cover;
}
</style>
