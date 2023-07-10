<script lang="ts" setup>
const products = ref([
    { id: 1, title: "title 1", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999 },
    { id: 2, title: "title 2", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999 },
]);
definePageMeta({
    layout: "main"
})
</script>

<template>
    <div id="ShoppingCartPage" class="mt-4 max-w-[1200px] mx-auto px-2">
        <div v-if="false" class="h-[500px] flex items-center justify-center">
            <div class="pt-20">
                <img class="mx-auto" width="250" src="/cart-empty.png" />

                <h3 class="text-xl text-center mt-4">No Items yet?</h3>

                <div v-if="true" class="flex text-center">
                    <NuxtLink to="/auth" class="bg-primary w-full text-white text-xl font-semibold rounded-full mt-4">Sign
                        In</NuxtLink>
                </div>
            </div>
        </div>
        <div v-else class="md:flex gap-4 justify-between mx-auto w-full">
            <section class="md:w-[65%]">
                <div class="bg-white rounded-lg p-4">
                    <span class="text-2xl font-bold mb-2">
                        Shopping Cart (0)
                    </span>
                </div>
                <div class="bg-[#FEEEEF] rounde-lg p-4 mt-4">
                    <span class="text-red-500 font-bold">
                        Welcome Deal applicable on 1 Item only
                    </span>
                </div>
                <div id="Items" class="bg-white rounded-lg p-4 mt-4">
                    <div v-for="product in products" :key="product.id">
                        <CartShoppingItem 
                            :product="product"
                            :selectedArray="selectedArray"
                            @selectedRadio="selectedRadioFunc"
                        />
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>
