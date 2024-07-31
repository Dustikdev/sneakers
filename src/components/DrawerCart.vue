<script setup>

defineProps({
    id: Number,
    imageUrl: String,
    title: String,
    price: Number,
})

const emit = defineEmits(['onClickRemove']);

</script>

<template>
    <div class="flex items-center border border-slate-100 rounded-xl p-4 gap-4">
        <img class="w-16 h-16" :src="imageUrl" alt="sneaker">
        <div class="flex flex-col justify-between">
            <p>{{ title }}</p>
            <div class="flex justify-between mt-2">
                <b>{{ price }} руб.</b>
                <img @click="emit('onClickRemove')" class="opacity-30 hover:opacity-100 cursor-pointer transition"
                    src="/close.svg" alt="close">
            </div>
        </div>
    </div>
</template>