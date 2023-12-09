<script setup>
import HeaderLinkItem from '../HeaderLinkItem/HeaderLinkItem.vue'

const HEADER_LIST_ITEMS = [
  {
    path: '/cart.svg',
    alt: 'Cart',
    text: 'Cart'
  },
  {
    path: '/heart.svg',
    alt: 'Bookmark',
    text: 'Bookmark'
  },
  {
    path: '/profile.svg',
    alt: 'Profile',
    text: 'Profile'
  }
]
</script>

<template>
  <ul class="flex items-center gap-10">
    <HeaderLinkItem
      v-for="(item, index) in HEADER_LIST_ITEMS"
      :key="index"
      :path="item.path"
      :alt="item.alt"
      :text="item.text"
    />
  </ul>
</template>
