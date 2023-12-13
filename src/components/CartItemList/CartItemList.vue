<script setup>
import CartItem from '../CartItem/CardItem.vue'
import { inject } from 'vue'

const { cart, removeFromCart } = inject('cart')

const onClickRemove = (item) => {
  removeFromCart(item)
}
</script>

<template>
  <div class="flex flex-col gap-4" v-auto-animate>
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :title="item.title"
      :price="item.price"
      :imageUrl="item.imageUrl"
      @on-click-remove="() => onClickRemove(item)"
    />
  </div>
</template>
