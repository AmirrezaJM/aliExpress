<script setup>
definePageMeta({
  layout: "main",
});
const products = ref([
  {id: 1, title: "title 1", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999},
  {id: 2, title: "title 2", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999},
  {id: 3, title: "title 3", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999},
  {id: 4, title: "title 4", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999},
  {id: 5, title: "title 5", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999},
  {id: 6, title: "title 6", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999},
  {id: 7, title: "title 7", description: "lorem lorem lorem", url: "https://picsum.photos/id/7/800/800", price: 9999},
])
</script>

<template>
    <div id="IndexPage" class="container mt-4 max-w-[1200px] mx-auto px-2">
      <div class="grid xl:grid-cols-6 lg:grid-cols-5 md:grid-cols-4 sm:grid-cols-3 grid-cols-2 gap-4">
          <div v-if="products" v-for="product in products" :key="product.id">
            <Product :product="product" />
          </div>
      </div>
    </div>
</template>
