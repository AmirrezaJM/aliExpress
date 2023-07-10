<script setup>
    import { useUserStore } from '~/stors/user';
    const userStore = useUserStore()
    const props = defineProps(["product","selectedArray"])
    const { product,selectedArray } = toRefs(props)
    const emit = ​defineEmits(['selectedRadio']);
    let isHover = ref(false)
    let isSelected = ref(false) 
    

    const removeFromCart = () => {
        userStore.cart.forEach((prod,index) => {
            if(prod.id === product.value.id) {
                userStore.cart.splice(index,1)
            }
        })
    }

    watch(() => isSelected.value, (val) => {
        emit('selectedRadio', {id: product.value.id,val:val})
    })
</script>

<template>
    <div class="flex justify-start my-2">
        <div class="my-auto">
            <div
                @mouseenter="isHover = true"
                @mouseleave="isHover = false"
                class="flex items-center justify-start p-0.5 curor-pointer"
            >
                <div
                    @click="isSelected = !isSelected"
                    class="flex items-center justify-center h-[20px] w-[20px] rounded-full border mr-5 ml-2"
                    :class="[
                        isHover ? 'border-primary' : 'border-gray-300',
                        isSelected ? 'bg-primary' : ''
                    ]"
                >
                    <div class="h-2 w-2 rounded-full bg-white"></div>
                </div>
            </div>
        </div>
        <img 
            class="rounded-md md:w-[150px] w-[90px]"
            :src="product.url"
        />
        <div class="overflow-hidden pl-2 w-full">
            <div class="flex items-center justify-between w-full">
                <div class="flex items-center justify-between truncate">
                    <span class="sm:block hidden bg-primary text-white text-sm font-semibold rounded-sm min-w-[80px]">Welcome Deal</span>
                </div>
            </div>
        </div>
    </div>
</template>
