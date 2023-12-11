<script setup>
import CartItem from '../CartItem/CardItem.vue'
</script>

<template>
  <div class="flex flex-col gap-4">
    <CartItem title="Sneaker Nike" :price="3400" imageUrl="/sneakers/sneakers-1.jpg" />
    <CartItem title="Sneaker Nike" :price="3400" imageUrl="/sneakers/sneakers-2.jpg" />
    <CartItem title="Sneaker Nike" :price="3400" imageUrl="/sneakers/sneakers-3.jpg" />
  </div>
</template>
