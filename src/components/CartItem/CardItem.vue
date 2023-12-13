<script setup>
defineProps({
  imageUrl: String,
  title: String,
  price: Number
})

const emit = defineEmits(['onClickRemove'])
</script>

<template>
  <div class="flex items-center border border-slate-200 p-4 rounded-xl gap-4">
    <img class="w-16 h-16" :src="imageUrl" :alt="title" />

    <div class="flex flex-col flex-1">
      <p>{{ title }}</p>

      <div class="flex justify-between mt-2">
        <b class="flex-1">${{ price }}</b>
        <img
          src="/close.svg"
          class="opacity-40 cursor-pointer transition hover:opacity-100"
          alt="Remove"
          @click="emit('onClickRemove')"
        />
      </div>
    </div>
  </div>
</template>
