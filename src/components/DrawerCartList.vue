<script setup>
import DrawerCart from "./DrawerCart.vue";
import { inject } from "vue";

const { drawerItems, deleteFromCart } = inject('cart');

</script>

<template>
    <div class="flex flex-col gap-4">
        <DrawerCart v-for="item in drawerItems" :key="item.id" :id="item.id" :image-url="item.imageUrl"
            :title="item.title" :price="item.price" @on-click-remove="() => deleteFromCart(item)" />
    </div>
</template>