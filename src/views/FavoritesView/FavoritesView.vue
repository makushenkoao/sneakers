<script setup>
import CardList from '@/components/CardList/CardList.vue'
import { onMounted, ref } from 'vue'
import axios from 'axios'
import { __API__ } from '@/assets/consts.js'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(`${__API__}/favorites?_relations=items`)

    favorites.value = data.map((obj) => obj.item)
  } catch (err) {
    console.log(err)
  }
})
</script>
<template>
  <h2 class="text-3xl font-bold mb-8">My bookmarks</h2>

  <CardList :items="favorites" is-favorites />
</template>
