<template>

    <!-- Desktop sidebar -->
    <aside :class="{'hidden':!isSideMenuOpen}"
           class="z-20  w-64 overflow-y-auto bg-gray-800 dark:bg-gray-800  flex-shrink-0">
        <div class="py-4 text-gray-200 dark:text-gray-400">
            <a class="ml-6 text-lg font-bold text-gray-100 dark:text-gray-200"
               href="#">
                Windmill
            </a>

            <ul class="mt-6">
                <SideNavItem
                    :href="route('dashboard')"
                    name="Dashboard"
                    :active="route().current('dashboard')">
                    <HomeIcon class="w-5 h-5"/>
                </SideNavItem>
                <SideNavItem
                    name="Forms">
                    <ClipboardIcon class="w-5 h-5"/>
                </SideNavItem>

                <SideNavMultiList name="Setting" :active="false">
                    <template v-slot:trailingIcon>
                        <CogIcon class="w-5 h-5"/>
                    </template>
                    <SubMenuItem>Users</SubMenuItem>
                    <SubMenuItem>Permissions</SubMenuItem>
                    <SubMenuItem>Roles</SubMenuItem>
                    <SubMenuItem>Change Password</SubMenuItem>
                </SideNavMultiList>
            </ul>
            <div class="px-6 my-6">
                <button
                    class="flex items-center justify-between w-full px-4 py-2 text-sm font-medium leading-5 text-white transition-colors duration-150 bg-blue-600 border border-transparent rounded-lg active:bg-blue-600 hover:bg-blue-700 focus:outline-none focus:shadow-outline-blue"
                >
                    Create account
                    <span class="ml-2" aria-hidden="true">+</span>
                </button>
            </div>
        </div>
    </aside>
    <!-- Mobile sidebar -->
    <!-- Backdrop -->
    <Transition
        enter-active-class="transition ease-in-out duration-150"
        enter-from-class="opacity-0"
        enter-to-class="opacity-100"
        leave-active-class="transition ease-in-out duration-150"
        leave-from-class="opacity-100"
        leave-to-class="opacity-0">
        <div v-show="isSideMenuOpen"
             class="fixed inset-0 z-10 flex items-end bg-black bg-opacity-50 md:bg-transparent md:opacity-100 sm:items-center sm:justify-center"></div>
    </Transition>

</template>

<script setup>
import SideNavItem from "../Components/SideNavItem.vue";
import SideNavMultiList from "../Components/SideNavMultiList.vue";
import SubMenuItem from "../Components/SubMenuItem.vue";

import {MoonIcon, HomeIcon, ClipboardIcon, CogIcon} from '@heroicons/vue/solid';

defineProps({
    isSideMenuOpen: {
        type: Boolean,
        default: true
    }
})


</script>

<style scoped>

</style>
