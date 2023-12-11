<script setup>
import Drawer from '../Drawer/Drawer.vue'
import CartItemList from '@/components/CartItemList/CartItemList.vue'
const emit = defineEmits(['onClose'])
</script>

<template>
  <Drawer @on-close="emit('onClose')">
    <h2 class="text-2xl font-bold mb-4">Cart</h2>
    <CartItemList />
    <div class="flex flex-col gap-4 mt-10">
      <div class="flex gap-2">
        <span>Total:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>$570</b>
      </div>
      <div class="flex gap-2">
        <span>Tax 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>$30</b>
      </div>
      <button
        class="bg-blue-400 w-full rounded-xl py-3 text-white disabled:bg-slate-400 hover:bg-blue-600 active:bg-blue-700 transition"
      >
        Checkout
      </button>
    </div>
  </Drawer>
</template>
