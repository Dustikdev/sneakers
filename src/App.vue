<script setup>
import MainHeader from "./components/MainHeader.vue";
import CardList from "./components/CardList.vue";
import Drawer from "./components/Drawer.vue";
import { onMounted, ref, watch, reactive, provide } from "vue";
import axios from "axios";

const items = ref([]);
const drawerItems = ref([]);
const totalPrice = ref(0);

const drawerOpen = ref(false);

const filters = reactive({
  sortBy: '',
  searchBy: '',
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value;
}

const onChangeSearchInput = (event) => {
  filters.searchBy = event.target.value;
}

const openDrawer = () => {
  drawerOpen.value = true
}

const closeDrawer = () => {
  drawerOpen.value = false
}

const onClickAddPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    deleteFromCart(item)
  }
  // console.log(drawerItems.value);
}

const addToCart = (item) => {
  drawerItems.value.push(item)
  totalPrice.value += item.price
  item.isAdded = true
}

const deleteFromCart = (item) => {
  drawerItems.value.splice(drawerItems.value.indexOf(item), 1)
  totalPrice.value -= item.price
  item.isAdded = false
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://4d196ee24aeee904.mokky.dev/favorites');
    items.value = items.value.map((item => {
      const favorite = favorites.find((favorite) => favorite.parentId === item.id)
      if (!favorite) {
        return item
      }
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    }))
    // console.log(items.value)
  } catch (error) {
    console.error('There was a problem with the fetch operation:', error);
  }
}

const fetchItems = async () => {
  const url = 'https://604781a0efa572c1.mokky.dev/items';
  const params = {}
  if (filters.sortBy) {
    params.sortBy = filters.sortBy
  }
  if (filters.searchBy) {
    params.title = `*${filters.searchBy}*`
  }
  try {
    const { data } = await axios.get(url, { params });
    items.value = data.slice(0, 12).map((obj) => {
      return {
        ...obj,
        // isFavorite: false,
        isAdded: false,
        favoriteId: null
      }
    })
    // console.log(items.value)
  } catch (error) {
    console.error('There was a problem with the fetch operation:', error);
  }
}

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        parentId: item.id
      }
      item.isFavorite = true
      const { data } = await axios.post('https://4d196ee24aeee904.mokky.dev/favorites', obj);
      item.favoriteId = data.id
      console.log(data)
    } else {
      item.isFavorite = false
      await axios.delete(`https://4d196ee24aeee904.mokky.dev/favorites/${item.favoriteId}`);
      delete item.favoriteId
    }
  } catch (error) {
    console.log(error)
  }

  // console.log(item);
}

onMounted(async () => {
  await fetchItems();
  await fetchFavorites();
});

watch(filters, async () => {
  await fetchItems();
  await fetchFavorites();
});

provide('cart', { closeDrawer, drawerItems, deleteFromCart, addToCart })

</script>

<template>
  <Drawer v-if="drawerOpen" />
  <div class="w-4/5 mx-auto bg-white rounded-xl shadow-xl mt-10">
    <MainHeader @open-drawer="openDrawer" :total-price="totalPrice" />
    <div class="p-10">
      <div class="flex justify-between items-center mb-10 gap-4">
        <h2 class="text-3xl font-bold">Все кроссовки</h2>
        <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
          <option value="name">По названию</option>
          <option value="price">По цене (дешевые)</option>
          <option value="-price">По цене (дорогие)</option>
        </select>
        <div class="relative">
          <img class="absolute left-3 top-3" src="/search.svg" alt="search">
          <input @input="onChangeSearchInput"
            class="border rounded-md py-2 pl-10 pr-4 outline-none focus:border-gray-400" type="text"
            placeholder="Поиск...">
        </div>
      </div>
      <CardList :items="items" @add-to-favorite="addToFavorite" @on-click-add-plus="onClickAddPlus" />
    </div>
  </div>
</template>
