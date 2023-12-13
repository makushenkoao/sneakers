<script setup>
import Card from '@/components/Card/Card.vue'

defineProps({
  items: Array,
  isFavorites: Boolean
})

const emit = defineEmits(['addToFavorite', 'addToCart'])

const onClickFavorite = (item) => {
  emit('addToFavorite', item)
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5" v-auto-animate>
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :image-url="item.imageUrl"
      :title="item.title"
      :price="item.price"
      :is-favorite="item.isFavorite"
      :is-added="item.isAdded"
      :on-click-favorite="isFavorites ? null : () => onClickFavorite(item)"
      :on-click-add="isFavorites ? null : () => emit('addToCart', item)"
    />
  </div>
</template>
