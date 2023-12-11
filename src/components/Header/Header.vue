<script setup>
const emit = defineEmits(['openDrawer'])
</script>

<template>
  <header class="flex justify-between border-b border-slate-100 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl uppercase font-bold">vue sneakers</h2>
        <p class="text-slate-400">Shop the best sneakers</p>
      </div>
    </div>
    <ul class="flex items-center gap-10">
      <li
        class="flex items-center gap-3 text-slate-500 cursor-pointer hover:text-black"
        @click="() => emit('openDrawer')"
      >
        <img src="/cart.svg" alt="Cart" />
        <span>$600</span>
      </li>
      <li class="flex items-center gap-3 text-slate-500 cursor-pointer hover:text-black">
        <img src="/heart.svg" alt="Bookmark" />
        <span>Bookmark</span>
      </li>
      <li class="flex items-center gap-3 text-slate-500 cursor-pointer hover:text-black">
        <img src="/profile.svg" alt="Profile" />
        <span>Profile</span>
      </li>
    </ul>
  </header>
</template>
