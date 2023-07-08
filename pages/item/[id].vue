<script setup>
const images = ref([
    '',
    'https://picsum.photos/id/7/800/800',
    'https://picsum.photos/id/12/800/800',
    'https://picsum.photos/id/23/800/800',
    'https://picsum.photos/id/432/800/800',
    'https://picsum.photos/id/124/800/800',
    'https://picsum.photos/id/34/800/800',
]);

watchEffect(() => {
  images.value[0] = "https://picsum.photos/id/77/800/800"
});
definePageMeta({
    layout: 'main'
})
</script>

<template>
    <div id="ItemPage" class="container mt-4 max-w-[1200px] mx-auto px-2">
        <div class="md:flex gap-4 justify-between mx-auto w-full">
            <div class="md:w-[40%]">
                <img 
                    class="rounded-lg object-fit"
                    src="https://picsum.photos/id/43/800/800"
                />
                <div v-if="images[0] !== ''" class="flex justify-center items-center mt-2">
                    <div v-for="image in images">
                        <img 
                            @mouseover="currentImage = image"
                            @click="currentImage = image"
                            width="70"
                            class="rounded-md object-fit border-[3px] cursor-pointer"
                            :class="currentImage === image ? 'border-primary': ''"
                            :src="image"
                        />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
