<script setup>
import HeaderLinkList from './HeaderLinkList/HeaderLinkList.vue'
</script>

<template>
  <header class="flex justify-between border-b border-slate-300 px-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl uppercase font-bold">vue sneakers</h2>
        <p class="text-slate-400">Магазин лучших кросовок</p>
      </div>
    </div>
    <HeaderLinkList />
  </header>
</template>
