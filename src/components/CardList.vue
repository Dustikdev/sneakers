<script setup>
import ProductCard from "./ProductCard.vue";

defineProps({
  items: Array,
});

const emit = defineEmits(['addToFavorite', 'onClickAddPlus'])

</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <ProductCard v-for="item in items" :key="item.id" :id="item.id" :price="item.price" :title="item.title"
      :image-url="item.imageUrl" :is-favorite="item.isFavorite" :is-added="item.isAdded"
      :onClickToFavorite="() => $emit('addToFavorite', item)" :onClickToAdded="() => $emit('onClickAddPlus', item)" />
  </div>
</template>