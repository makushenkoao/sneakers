<script setup>
import Card from '@/components/Card/Card.vue'

defineProps({
  items: Array
})

const emit = defineEmits(['addToFavorite'])

const onClickFavorite = (item) => {
  emit('addToFavorite', item)
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :imageUrl="item.imageUrl"
      :title="item.title"
      :price="item.price"
      :isFavorite="item.isFavorite"
      :isAdded="item.isAdded"
      :onClickFavorite="() => onClickFavorite(item)"
    />
  </div>
</template>
