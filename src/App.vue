<script setup>
import Header from '@/components/Header/Header.vue'
import CardList from '@/components/CardList/CardList.vue'
import debounce from 'lodash.debounce'
import DrawerCart from '@/components/DrawerCart/DrawerCart.vue'
import axios from 'axios'
import { onMounted, reactive, ref, watch, provide } from 'vue'

const url = 'https://2a9a43aa256890e4.mokky.dev'

const items = ref([])

const isOpenDrawer = ref(false)

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = debounce((event) => {
  filters.searchQuery = event.target.value
}, 300)

const openDrawer = () => {
  isOpenDrawer.value = true
}

const closeDrawer = () => {
  isOpenDrawer.value = false
}

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        item_id: item.id
      }

      item.isFavorite = true

      const { data } = await axios.post(`${url}/favorites`, obj)

      item.favoriteId = data.id
    } else {
      item.isFavorite = false
      await axios.delete(`${url}/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }
  } catch (err) {
    console.log(err)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`${url}/favorites`)

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.item_id === item.id)

      if (!favorite) {
        return item
      }

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })
  } catch (err) {
    console.log(err)
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(`${url}/items`, {
      params
    })

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      isAdded: false
    }))
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()

  // items.value = items.value.map((item) => ({
  //   ...item,
  //   isAdded: cart.value.some((cartItem) => cartItem.id === item.id)
  // }))
})

watch(filters, fetchItems)

provide('cartActions', {
  closeDrawer,
  openDrawer
})
</script>

<template>
  <DrawerCart v-if="isOpenDrawer" @on-close="closeDrawer" />

  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header @open-drawer="openDrawer" />
    <div class="p-10">
      <div class="flex justify-between items-center mb-10">
        <h2 class="text-3xl font-bold">All sneakers</h2>
        <div class="flex gap-4 items-center">
          <select class="py-2 px-3 border rounded-md outline-none" @change="onChangeSelect">
            <option value="title">By name</option>
            <option value="-price">By price (⬆)</option>
            <option value="price">By price (⬇)</option>
          </select>
          <div class="relative">
            <img src="/search.svg" alt="Search" class="absolute left-3 top-3 bottom-0.5" />
            <input
              @change="onChangeSearchInput"
              type="text"
              placeholder="Search..."
              class="border rounded-md py-2 pl-10 px-4 outline-none focus:border-gray-400"
            />
          </div>
        </div>
      </div>
      <CardList :items="items" @add-to-favorite="addToFavorite" />
    </div>
  </div>
</template>

<style scoped></style>
