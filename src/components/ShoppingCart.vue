<template>
  <div class="">
    <div class="contain justify-content-between">
      <h6 class="my-0">{{ product.name }}</h6>
      <p class="text-muted">數量：{{ product.quantity }}</p>
      <p class="text-muted">${{ product.price }}</p>
      <button class="btn btn-sm btn-outline-danger ms-2" @click="removeFromCart">移除</button>
    </div>
  </div>
</template>
<script setup>
import { inject } from 'vue'
const product = defineProps(['id', 'name', 'price', 'image', 'description', 'quantity'])
console.log('product in ShoppingCart=>', product)

const emit = defineEmits(['emitRemoveFromCart'])
const removeFromCart = () => {
  //console.log('移除購物車')
  injectedMessage.value=product.name+'<=從購物車移除'
  injectedGreet(injectedMessage)
  emit('emitRemoveFromCart', product)
}
// Inject the message
const injectedMessage = inject('messageKey')
// Inject the greet function
const injectedGreet = inject('greetFunctionKey')

</script>
<style scoped>
.contain {
  border: 1px solid #ccc;
}
.card-img-top {
  height: 150px;
  object-fit: cover;
}
.btn {
  border: 1px solid #ccc;
  color: red;
}
</style>
