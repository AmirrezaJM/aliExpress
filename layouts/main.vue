<script setup>
import { useUserStore } from '~/stores/user';
const userStore = useUserStore();
const isAccountMenu = ref(false);
const searchItem = ref('');
const isSearching = ref(false);
const isCartHover = ref(false);
</script>

<template>
    <div id="mainLayout" class="w-full fixed z-50">
        <div id="topMenu" class="w-full bg-background md:block hidden">
            <ul
                class="flex items-center justify-end text-xs text-slate-400 font-light px-2 h-10 border-b bg-background max-w-[1200px]">
                <li class="border-r border-r-gray-400 px-3 hover:text-primary cursor-pointer">
                    Sell on AliExpress
                </li>
                <li class="border-r border-r-gray-400 px-3 hover:text-primary cursor-pointer">
                    Cookie Preferences
                </li>
                <li class="border-r border-r-gray-400 px-3 hover:text-primary cursor-pointer">
                    Help
                </li>
                <li class="border-r border-r-gray-400 px-3 hover:text-primary cursor-pointer">
                    Buyer Protection
                </li>
                <li class="px-3 hover:text-primary cursor-pointer">
                    <Icon name="ic:sharp-install-mobile" size="17" />
                    App
                </li>
                <li @mouseenter="isAccountMenu = true" @mouseleave="isAccountMenu = false"
                    class="relative flex items-center px-2.5 hover:text-primary h-full cursor-pointer"
                    :class="isAccountMenu ? 'bg-white border z-40 shadow[0_15px_100px_40px_rgba(0,0,0,0.3)]' : 'border border-background'">
                    <Icon name="ph:user-thin" size="17" />
                    Account
                    <Icon name="mdi:chevron-down" size="15" class="ml-5" />
                    <div id="AccountMenu" v-if="isAccountMenu"
                        class="absolute bg-white w-[220px] text-gray-900 z-40 top-[30px] -left-[100px] border-x border-b">
                        <div v-if="true">
                            <div class="text-semibold text-sm my-4 px-3">Welcome to AliExpress</div>
                            <div class="flex items-center gap-1 px-3 mb-3">
                                <NuxtLink to="/auth"
                                    class="bg-primary text-center text-sm rounded-sm text-white font-semibold p-2 w-full">
                                    Login/ Register
                                </NuxtLink>
                            </div>
                        </div>
                        <div class="border-b">
                            <ul class="bg-white">
                                <li @click="navigateTo('/orders')" class="text-xs py-2 px-4 w-full hover:bg-gray-200">
                                    My Orders
                                </li>
                                <li v-if="true" class="text-xs py-2 px-4 w-full hover:bg-gray-200">
                                    Sign out
                                </li>
                            </ul>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
        <div id="MainHeader" class="flex items-center w-full bg-white">
            <div class="flex lg:justify-start justify-between gap-10 max-w-[1150px] w-full px-3 py-5 mx-auto">
                <NuxtLink to="/" class="min-w-[170px]">
                    <img width="170" src="/AliExpress-logo.png" />
                </NuxtLink>
                <div class="max-w-[700px] w-full md:block hidden">
                    <div class="flex items-center border-2 border-primary rounded-md w-full">
                        <input class="w-full placeholder-gray-400 text-sm pl-3 focus:outline-none"
                            placeholder="kitchen accessories" type="text" v-model="searchItem" />
                        <Icon v-if="isSearching" name="eos-icons:loading" size="25" class="mr-2" />
                        <button class="flex items-center h-full p-1.5 px-2 bg-primary">
                            <Icon name="ph:magnifying-glass" size="20" color="#fff" />
                        </button>
                    </div>
                    <div class="absolute bg-white max-w-[700px] h-auto w-full">
                        <div v-if="false" class="p-1">
                            <NuxtLink to="`/item/1`"
                                class="flex items-center justify-between cursor-pointer bg-white hover:bg-gray-100">
                                <div class="flex items-center">
                                    <img class="rounded-md" width="40" src="https://picsum.photos/id/82/300/300" />
                                    <div class="truncate ml-2">Testing</div>
                                </div>
                                <div class="truncate">$ 98.99</div>
                            </NuxtLink>
                        </div>
                    </div>
                </div>
                <NuxtLink to="/shoppingcart" class="flex items-center">
                    <button
                        class="relative md:block hidden"
                        @mouseenter="isCartHover = true"
                        @mouseleave="isCartHover = false"
                    >
                        <span class="absolute flex items-center justify-center -right-[3px] top-0 bg-primary h-17 min-w-[17px] text-sm text-white px-0.5 rounded-full">
                            0
                        </span>
                        <div class="min-w-[40px]">
                            <Icon name="ph:shopping-cart-simple-light" size="33" :color="isCartHover ? '#FF4646': ''"/>
                        </div>
                    </button>
                </NuxtLink>
                <button
                    @click="userStore.isMenuOverlay = true"
                    class="md:hidden block rounded-full p-1.5 -mt-4 hover:bg-gray-100">
                    <Icon name="radix-icons:hamburger-menu" size="33"/>
                </button>
            </div>
        </div>
    </div>

    <Loading v-if="userStore.isLoading" />
    <div class="lg:pt-[150px] md:pt-[130px] pt-[80px]"></div>
    <slot />

    <Footer v-if="!userStore.isLoading" />
</template>

