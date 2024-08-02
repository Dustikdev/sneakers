<script setup>
import { inject } from "vue";

defineProps({
    title: String,
    description: String,
    imageUrl: String
})

const { closeDrawer } = inject('cart')

</script>


<template>
    <div class="flex flex-grow flex-col justify-center items-center gap-8">
        <img class="w-40 h-40" :src="imageUrl" alt="info image">
        <h2 class="text-2xl font-bold">{{ title }}</h2>
        <p class="text-slate-400 text-xl text-center">{{ description }}</p>
        <button @click='closeDrawer'
            class="group flex gap-4 justify-center items-center text-xl bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 transition active:bg-lime-700 disabled:bg-slate-300 cursor-pointer mt-2">
            <svg class="cursor-pointer rotate-180 hover:opacity-100 group-hover:-translate-x-1 transition" width="16"
                height="14" viewBox="0 0 16 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M1 7H14.7143" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M8.71436 1L14.7144 7L8.71436 13" stroke="white" stroke-width="2" stroke-linecap="round"
                    stroke-linejoin="round" />
            </svg>
            Вернуться назад
        </button>
    </div>
</template>
