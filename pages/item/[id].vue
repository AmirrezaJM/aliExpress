<script setup>
import { useUserStore } from '~/stores/user';
const userStore = useUserStore();
const route = useRoute();
const currentImage = ref(null)
const images = ref([
    '',
    'https://picsum.photos/id/7/800/800',
    'https://picsum.photos/id/12/800/800',
    'https://picsum.photos/id/23/800/800',
    'https://picsum.photos/id/432/800/800',
    'https://picsum.photos/id/124/800/800',
    'https://picsum.photos/id/34/800/800',
]);

const priceComputed = computed(() => {
    return '26.50'
})

onMounted(() => {
    watchEffect(() => {
        currentImage.value = "https://picsum.photos/id/77/800/800"
        images.value[0] = "https://picsum.photos/id/77/800/800"
    });    
});

const isInCart = computed(() => {
    let res = false
    userStore.cart.forEach(prod => {
        if(route.params.id === prod.id) {
            res = true
        }
    })

    return res
})
const addToCart = () => {
    alert('ADDED')
}

definePageMeta({
    layout: 'main'
});
</script>

<template>
    <main id="ItemPage" class="container mt-4 max-w-[1200px] mx-auto px-2">
        <div class="md:flex gap-4 justify-between mx-auto w-full">
            <div class="md:w-[40%]">
                <img 
                    class="rounded-lg object-fit"
                    :src="currentImage"
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
            <div class="md:w-[60%] bg-white p-3 rounded-lg">
                <div v-if="true">
                    <p class="mb-2">Title</p>
                    <p class="font-light text-xs mb-2">Description section</p>
                </div>
                <div class="flex items-center my-2">
                    <span class="h-4 w-4 rounded-full p-0.5 bg-[#FFD000] mr-2">
                        <Icon name="material-symbols:star-rounded" color="#fff" class="-mr-[17px]" size="12" style="display: block;" />
                    </span>
                    <p class="text-primary">Extra 5% off</p>
                </div>

                <div class="flex items-center justify-start">
                    <Icon name="material-symbols:star-rounded" color="#FF5353" />
                    <Icon name="material-symbols:star-rounded" color="#FF5353" />
                    <Icon name="material-symbols:star-rounded" color="#FF5353" />
                    <Icon name="material-symbols:star-rounded" color="#FF5353" />
                    <Icon name="material-symbols:star-rounded" color="#FF5353" />
                    <span class="text-xs font-light ml-2">5 213 Reviews 1.000+ orders</span>
                </div>

                <div class="border-b"></div>

                <div class="flex items-center justify-start gap-2 my-2">
                    <div class="text-xl font-bold">
                        {{ priceComputed }}
                    </div>
                    <div class="bg-[#F5F5F5] border text-secondary text-[9px] font-semibold px-1.5 rounded-sm">70% off</div>
                </div>

                <p class="text-[#009A66] text-xs font-semibold pt-1">
                    Free 11-day delivery over $8.28
                </p>

                <p class="text-[#009A66] text-xs font-semibold pt-1">
                    Free shipping
                </p>

                <div class="py-2" />

                <button
                    @click="addToCart()"
                    :disabled="isInCart"
                    class="px-6 py-2 rounded-lg text-white text-lg font-semibold bg-gradient-to-r from-[#FF851A] to-[#FFAC2C]"
                >    
                    <div v-if="isInCart">Is Added</div>
                    <div v-else>Add To Cart</div>
                </button>
            </div>
        </div>
    </main>
</template>
