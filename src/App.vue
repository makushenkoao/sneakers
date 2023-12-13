<script setup>
// Если добавить товар в корзину, перезагрузить страницу и удалить товар из корзины, то isAdded не меняется - пофиксить
import Header from '@/components/Header/Header.vue'
import DrawerCart from '@/components/DrawerCart/DrawerCart.vue'
import axios from 'axios'
import { computed, provide, ref, watch } from 'vue'
import { __API__ } from '@/assets/consts.js'

const cart = ref([])
const isOpenDrawer = ref(false)

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrice = computed(() => Math.round((totalPrice.value * 5) / 100))

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAdded = false
}

const openDrawer = () => {
  isOpenDrawer.value = true
}

const closeDrawer = () => {
  isOpenDrawer.value = false
}

watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  { deep: true }
)

provide('cart', {
  cart,
  closeDrawer,
  openDrawer,
  addToCart,
  removeFromCart
})
</script>

<template>
  <DrawerCart v-if="isOpenDrawer" :total-price="totalPrice" :vat-price="vatPrice" />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header @open-drawer="openDrawer" :total-price="totalPrice" />
    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>

<style scoped></style>
