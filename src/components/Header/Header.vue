<script setup>
defineProps({
  totalPrice: Number
})

const emit = defineEmits(['openDrawer'])
</script>

<template>
  <header class="flex justify-between border-b border-slate-100 px-10 py-8">
    <router-link to="/">
      <div class="flex items-center gap-4 cursor-pointer hover:opacity-60">
        <img src="/logo.png" alt="Logo" class="w-10" />
        <div>
          <h2 class="text-xl uppercase font-bold">vue sneakers</h2>
          <p class="text-slate-400">Shop the best sneakers</p>
        </div>
      </div>
    </router-link>
    <ul class="flex items-center gap-10">
      <li
        class="flex items-center gap-3 text-slate-500 cursor-pointer hover:text-black"
        @click="() => emit('openDrawer')"
      >
        <img src="/cart.svg" alt="Cart" />
        <span>${{ totalPrice || '0' }}</span>
      </li>
      <router-link to="/favorites">
        <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/heart.svg" alt="Cart" />
          <span>Bookmark</span>
        </li>
      </router-link>
      <li class="flex items-center gap-3 text-slate-500 cursor-pointer hover:text-black">
        <img src="/profile.svg" alt="Profile" />
        <span>Profile</span>
      </li>
    </ul>
  </header>
</template>
