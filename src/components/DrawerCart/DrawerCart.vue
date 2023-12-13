<script setup>
import { computed, inject, ref } from 'vue'
import axios from 'axios'
import { __API__ } from '@/assets/consts.js'
import Drawer from '../Drawer/Drawer.vue'
import CartItemList from '@/components/CartItemList/CartItemList.vue'
import InfoBlock from '@/components/InfoBlock/InfoBlock.vue'

const { totalPrice } = defineProps({
  totalPrice: Number,
  vatPrice: Number
})
const { cart, closeDrawer } = inject('cart')

const isCreatingOrder = ref(false)
const orderId = ref(null)

const createOrder = async () => {
  try {
    isCreatingOrder.value = true

    const { data } = await axios.post(`${__API__}/orders`, {
      items: cart.value,
      totalPrice
    })

    cart.value = []

    orderId.value = data.id
    return data
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}
const cartIsEmpty = computed(() => cart.value.length === 0)
const isLoading = computed(() => isCreatingOrder.value || cartIsEmpty.value)
</script>

<template>
  <Drawer @on-close="closeDrawer">
    <div class="flex flex-col h-full">
      <h2 class="text-2xl font-bold mb-4">Cart</h2>

      <!-- Cart content -->
      <div class="flex-1 overflow-auto">
        <div class="flex h-full items-center" v-if="cartIsEmpty">
          <InfoBlock
            title="Cart is empty"
            image-url="/package-icon.png"
            description="add at least one pair of sneakers to place your order"
          />
        </div>

        <CartItemList />
      </div>

      <div class="flex flex-col gap-4 my-10" v-if="!cartIsEmpty">
        <div class="flex gap-2">
          <span>Total:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>${{ totalPrice }}</b>
        </div>
        <div class="flex gap-2">
          <span>Tax (5%)</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>${{ vatPrice }}</b>
        </div>
        <button
          :disabled="isLoading"
          class="bg-blue-400 w-full rounded-xl py-3 text-white disabled:bg-slate-400 hover:bg-blue-600 active:bg-blue-700 transition"
          @click="createOrder"
        >
          Checkout
        </button>
      </div>
    </div>
  </Drawer>
</template>
