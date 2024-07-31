<script setup>

defineProps({
  totalPrice: Number
})

const emit = defineEmits(['openDrawer'])
</script>

<template>
  <header class="flex justify-between border-b border-slate-100 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="logo" class="w-10">
      <div>
        <h2 class="font-bold text-xl uppercase">Vue Sneakers</h2>
        <p class="text-slate-400">Магазин лучших кроссовок</p>
      </div>
    </div>
    <ul class="flex items-center text-gray-500 gap-4">
      <li class="flex gap-3 items-center hover:text-black cursor-pointer">
        <img src="/cart.svg" alt="cart">
        <b>{{ totalPrice }} руб.</b>
      </li>
      <li @click="$emit('openDrawer')" class="flex gap-3 items-center hover:text-black cursor-pointer">
        <img src="/heart.svg" alt="cart">
        <span>Закладки</span>
      </li>
      <li class="flex gap-3 items-center hover:text-black cursor-pointer">
        <img src="/profile.svg" alt="cart">
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>
