<script setup>

defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickToFavorite: Function,
  onClickToAdded: Function,
});

</script>

<template>
  <div class="flex">
    <div
      class="flex flex-col w-full relative bg-white border border-slate-100 rounded-xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition">
      <img @click="onClickToFavorite" class="absolute top-8 left-8" :src="isFavorite ? '/like-2.svg' : '/like-1.svg'"
        alt="like">
      <img class="max-w-64 max-h-52 self-center" :src="imageUrl" alt="sneaker">
      <p class="mt-2">{{ title }}</p>
      <div class="flex flex-1 justify-between mt-5 items-end">
        <div class="flex flex-col">
          <div class="text-slate-400">Цена</div>
          <b>{{ price }} руб.</b>
        </div>
        <img class="w-8" @click="onClickToAdded" :src="isAdded ? '/checked.svg' : '/plus.svg'" alt="plus">
      </div>
    </div>
  </div>
</template>