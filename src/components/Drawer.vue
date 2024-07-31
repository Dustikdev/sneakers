<script setup>
import DrawerCartList from "./DrawerCartList.vue";
import { inject } from "vue";

const { closeDrawer } = inject('cart')
</script>

<template>
    <div class="fixed top-0 left-0 h-full w-full z-10 bg-black opacity-70"></div>
    <div class="flex flex-col bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
        <div class="flex items-center gap-5 mb-6">
            <svg @click='closeDrawer'
                class="opacity-30 cursor-pointer rotate-180 hover:opacity-100 hover:-translate-x-1 transition"
                width="16" height="14" viewBox="0 0 16 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M1 7H14.7143" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M8.71436 1L14.7144 7L8.71436 13" stroke="black" stroke-width="2" stroke-linecap="round"
                    stroke-linejoin="round" />
            </svg>
            <h2 class="text-2xl font-bold">Корзина</h2>
        </div>
        <DrawerCartList />
        <div class="flex flex-col flex-1 justify-end gap-4 mb-4">
            <div class="flex gap-2">
                <span>Итого:</span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>12999 руб.</b>
            </div>
            <div class="flex gap-2">
                <span>Налог 5%:</span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>900 руб.</b>
            </div>
            <button disabled="false"
                class="bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 transition active:bg-lime-700 disabled:bg-slate-300 cursor-pointer mt-2">
                Оформить заказ
            </button>
        </div>
    </div>
</template>