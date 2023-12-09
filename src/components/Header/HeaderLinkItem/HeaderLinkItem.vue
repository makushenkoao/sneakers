<script setup>
defineProps({
  path: String,
  text: String,
  alt: String
})
</script>

<template>
  <li class="flex items-center gap-3 text-slate-500 cursor-pointer hover:text-black">
    <img :src="path" :alt="alt" />
    <span>{{ text }}</span>
  </li>
</template>
