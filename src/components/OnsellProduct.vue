<template>
  <div class="card">
    <div>
      <img :src="product.image" class="card-img-top" />
      <div class="card-body">
        <h5 class="card-title">{{ product.name }}</h5>
        <p class="card-text">{{ product.description }}</p>
        <p class="fw-bold text-primary">${{ product.price }}</p>
        <button class="btn btn-success w-100" @click="addToCart">加入購物車</button>
      </div>
    </div>
  </div>
</template>
<script setup>

import { defineEmits } from 'vue'
import { inject } from 'vue'

const product = defineProps(['id', 'name', 'price', 'image', 'description', 'quantity'])

const emit = defineEmits(['emitAddToCart'])
const addToCart = () => {
  // console.log('加入購物車')
  injectedMessage.value=product.name+'=>加入構物車'
  injectedGreet(injectedMessage)
  emit('emitAddToCart', product)
}
// Inject the message
const injectedMessage = inject('messageKey')
// Inject the greet function
const injectedGreet = inject('greetFunctionKey')

// Optional: Provide a default value if the key is not found
//const anotherValue = inject('nonExistentKey', 'Default Value')
</script>

<style scoped>
.card {
  width: 230px;
}

.card-img-top {
  height: 150px;
  object-fit: cover;
}
.btn {
  border: 1px solid #ccc;
}
</style>
