<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const emit = defineEmits(['onClose'])

const modalRef = ref(null)

const closeModal = () => {
  emit('onClose')
}
const onEscKey = (event) => {
  if (event.key === 'Escape') {
    closeModal()
  }
}

onMounted(() => {
  window.addEventListener('keydown', onEscKey)
})

onUnmounted(() => {
  window.removeEventListener('keydown', onEscKey)
})
</script>

<template>
  <div
    @click="() => emit('onClose')"
    class="fixed top-0 left-0 z-10 h-full w-full bg-black opacity-70 cursor-pointer"
  />
  <div class="fixed bg-white w-96 h-full right-0 bottom-0 z-20 p-8" ref="modalRef">
    <img
      src="/arrow-next.svg"
      alt="Close"
      class="opacity-30 cursor-pointer rotate-180 hover:opacity-100 transition hover:-translate-x-1 mb-5"
      @click="() => emit('onClose')"
    />
    <slot></slot>
  </div>
</template>
