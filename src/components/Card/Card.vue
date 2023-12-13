<script setup>
defineProps({
  id: Number,
  price: Number,
  title: String,
  imageUrl: String,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function
})
</script>

<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <img
      @click="onClickFavorite"
      :src="isFavorite ? '/like-2.svg' : '/like-1.svg'"
      alt="Like"
      class="absolute left-8 top-8"
      v-if="onClickFavorite"
    />
    <img :src="imageUrl" alt="Sneaker" />
    <p class="mt-2">{{ title }}</p>
    <div class="flex justify-between mt-5">
      <div class="flex gap-1 items-center">
        <span class="text-slate-400">Цена:</span>
        <span class="font-bold">${{ price }}</span>
      </div>
      <img
        @click="onClickAdd"
        :src="isAdded ? '/checked.svg' : '/plus.svg'"
        :alt="isAdded ? 'Plus' : 'Checked'"
        v-if="onClickAdd"
      />
    </div>
  </div>
</template>
