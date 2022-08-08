<script setup>
import {ref} from 'vue';

import SubMenuItem from "../Components/SubMenuItem.vue";

import {MoonIcon, HomeIcon, ClipboardIcon, CogIcon} from '@heroicons/vue/solid';
import {MoonIcon as OutlineMoonIcon} from '@heroicons/vue/outline';
import SideNavItem from "../Components/SideNavItem.vue";
import SideNavMultiList from "../Components/SideNavMultiList.vue";

let isSideMenuOpen = ref(true);
let isNotificationsMenuOpen = ref(false);
let isProfileMenuOpen = ref(false);


const getThemeFromLocalStorage = () => {

    // if user already changed the theme, use it
    let item = window.localStorage.getItem('dark');

    if (item) {
        return Boolean(item);
    }

    // else return their preferences
    return (
        !!window.matchMedia &&
        window.matchMedia('(prefers-color-scheme: dark)').matches
    )
}

const setThemeToLocalStorage = (value) => {
    window.localStorage.setItem('dark', value)
}

let dark = ref(getThemeFromLocalStorage());
let toggleTheme = () => {
    dark.value = !dark.value;
    setThemeToLocalStorage(dark.value);
};
let toggleSideMenu = () => {
    isSideMenuOpen.value = !isSideMenuOpen.value;
};
let closeSideMenu = () => {
    console.log('closeSideMenu');
    // isSideMenuOpen.value = false;
};

let toggleNotificationsMenu = () => {
    isNotificationsMenuOpen.value = !isNotificationsMenuOpen.value;
};
let closeNotificationsMenu = () => {
    isNotificationsMenuOpen.value = false;
};
let toggleProfileMenu = () => {
    isProfileMenuOpen.value = !isProfileMenuOpen.value;
};
let closeProfileMenu = () => {
    isProfileMenuOpen.value = false;
};


</script>

<template>
    <!--    <div>
            <div class="min-h-screen bg-gray-100">
                <nav class="bg-white border-b border-gray-100">
                    &lt;!&ndash; Primary Navigation Menu &ndash;&gt;
                    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                        <div class="flex justify-between h-16">
                            <div class="flex">
                                &lt;!&ndash; Logo &ndash;&gt;
                                <div class="shrink-0 flex items-center">
                                    <Link :href="route('dashboard')">
                                        <BreezeApplicationLogo class="block h-9 w-auto" />
                                    </Link>
                                </div>

                                &lt;!&ndash; Navigation Links &ndash;&gt;
                                <div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
                                    <BreezeNavLink :href="route('dashboard')" :active="route().current('dashboard')">
                                        Dashboard
                                    </BreezeNavLink>
                                </div>
                            </div>

                            <div class="hidden sm:flex sm:items-center sm:ml-6">
                                &lt;!&ndash; Settings Dropdown &ndash;&gt;
                                <div class="ml-3 relative">
                                    <BreezeDropdown align="right" width="48">
                                        <template #trigger>
                                            <span class="inline-flex rounded-md">
                                                <button type="button" class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition ease-in-out duration-150">
                                                    {{ $page.props.auth.user.name }}

                                                    <svg class="ml-2 -mr-0.5 h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                                                        <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
                                                    </svg>
                                                </button>
                                            </span>
                                        </template>

                                        <template #content>
                                            <BreezeDropdownLink :href="route('logout')" method="post" as="button">
                                                Log Out
                                            </BreezeDropdownLink>
                                        </template>
                                    </BreezeDropdown>
                                </div>
                            </div>

                            &lt;!&ndash; Hamburger &ndash;&gt;
                            <div class="-mr-2 flex items-center sm:hidden">
                                <button @click="showingNavigationDropdown = ! showingNavigationDropdown" class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:bg-gray-100 focus:text-gray-500 transition duration-150 ease-in-out">
                                    <svg class="h-6 w-6" stroke="currentColor" fill="none" viewBox="0 0 24 24">
                                        <path :class="{'hidden': showingNavigationDropdown, 'inline-flex': ! showingNavigationDropdown }" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                                        <path :class="{'hidden': ! showingNavigationDropdown, 'inline-flex': showingNavigationDropdown }" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                                    </svg>
                                </button>
                            </div>
                        </div>
                    </div>

                    &lt;!&ndash; Responsive Navigation Menu &ndash;&gt;
                    <div :class="{'block': showingNavigationDropdown, 'hidden': ! showingNavigationDropdown}" class="sm:hidden">
                        <div class="pt-2 pb-3 space-y-1">
                            <BreezeResponsiveNavLink :href="route('dashboard')" :active="route().current('dashboard')">
                                Dashboard
                            </BreezeResponsiveNavLink>
                        </div>

                        &lt;!&ndash; Responsive Settings Options &ndash;&gt;
                        <div class="pt-4 pb-1 border-t border-gray-200">
                            <div class="px-4">
                                <div class="font-medium text-base text-gray-800">{{ $page.props.auth.user.name }}</div>
                                <div class="font-medium text-sm text-gray-500">{{ $page.props.auth.user.email }}</div>
                            </div>

                            <div class="mt-3 space-y-1">
                                <BreezeResponsiveNavLink :href="route('logout')" method="post" as="button">
                                    Log Out
                                </BreezeResponsiveNavLink>
                            </div>
                        </div>
                    </div>
                </nav>

                &lt;!&ndash; Page Heading &ndash;&gt;
                <header class="bg-white shadow" v-if="$slots.header">
                    <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
                        <slot name="header" />
                    </div>
                </header>

                &lt;!&ndash; Page Content &ndash;&gt;
                <main>
                    <slot />
                </main>
            </div>
        </div>-->

    <div
        class="flex min-h-screen bg-gray-50 dark:bg-gray-900">

        <!-- Desktop sidebar -->
        <aside :class="{'hidden':!isSideMenuOpen}" v-click-outside="closeSideMenu"
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


        <div class="flex flex-col flex-1 w-full">
            <header class="z-10 py-4 bg-white shadow-sm dark:bg-gray-800">
                <div
                    class="container flex items-center justify-between h-full px-6 mx-auto text-blue-600 dark:text-blue-300">
                    <!-- Mobile hamburger -->
                    <button
                        class="p-1 mr-5 -ml-1 rounded-md  focus:outline-none focus:shadow-outline-blue"
                        @click="toggleSideMenu"
                        aria-label="Menu">
                        <svg
                            class="w-6 h-6"
                            aria-hidden="true"
                            fill="currentColor"
                            viewBox="0 0 20 20"
                        >
                            <path
                                fill-rule="evenodd"
                                d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
                                clip-rule="evenodd"
                            ></path>
                        </svg>
                    </button>
                    <!-- Search input -->
                    <div class="flex justify-center flex-1 lg:mr-32">
                        <div
                            class="relative w-full max-w-xl mr-6 focus-within:text-blue-500">
                            <div class="absolute inset-y-0 flex items-center pl-2">
                                <svg
                                    class="w-4 h-4"
                                    aria-hidden="true"
                                    fill="currentColor"
                                    viewBox="0 0 20 20"
                                >
                                    <path
                                        fill-rule="evenodd"
                                        d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                                        clip-rule="evenodd"
                                    ></path>
                                </svg>
                            </div>
                            <input
                                class="w-full pl-8 pr-2 text-sm text-gray-700 placeholder-gray-600 bg-gray-100 border-0 rounded-md dark:placeholder-gray-500 dark:focus:shadow-outline-gray dark:focus:placeholder-gray-600 dark:bg-gray-700 dark:text-gray-200 focus:placeholder-gray-500 focus:bg-white focus:border-blue-300 focus:outline-none focus:shadow-outline-blue form-input"
                                type="text"
                                placeholder="Search for projects"
                                aria-label="Search"
                            />
                        </div>
                    </div>
                    <ul class="flex items-center flex-shrink-0 space-x-6">
                        <!-- Theme toggler -->
                        <li class="flex">
                            <button
                                class="rounded-md focus:outline-none focus:shadow-outline-blue"
                                @click="toggleTheme"
                                aria-label="Toggle color mode"
                            >
                                <template v-if="!dark">
                                    <MoonIcon class="w-5 h-5"/>

                                </template>
                                <template v-if="dark">
                                    <OutlineMoonIcon class="w-5 h-5"/>

                                </template>
                            </button>
                        </li>
                        <!-- Notifications menu -->
                        <li class="relative">
                            <button
                                class="relative align-middle rounded-md focus:outline-none focus:shadow-outline-blue"
                                @click="toggleNotificationsMenu"
                                @keydown.esc="closeNotificationsMenu"
                                v-click-outside="closeNotificationsMenu"
                                aria-label="Notifications"
                                aria-haspopup="true">
                                <svg
                                    class="w-5 h-5"
                                    aria-hidden="true"
                                    fill="currentColor"
                                    viewBox="0 0 20 20"
                                >
                                    <path
                                        d="M10 2a6 6 0 00-6 6v3.586l-.707.707A1 1 0 004 14h12a1 1 0 00.707-1.707L16 11.586V8a6 6 0 00-6-6zM10 18a3 3 0 01-3-3h6a3 3 0 01-3 3z"
                                    ></path>
                                </svg>
                                <!-- Notification badge -->
                                <span
                                    aria-hidden="true"
                                    class="absolute top-0 right-0 inline-block w-3 h-3 transform translate-x-1 -translate-y-1 bg-red-600 border-2 border-white rounded-full dark:border-gray-800"
                                ></span>
                            </button>
                            <template v-if="isNotificationsMenuOpen">

                                <Transition
                                    leave-active-class="transition ease-in duration-150"
                                    leave-from-class="opacity-100"
                                    leave-to-class="opacity-0"
                                >
                                    <ul

                                        @click.away="closeNotificationsMenu"
                                        @keydown.esc="closeNotificationsMenu"
                                        class="absolute right-0 w-56 p-2 mt-2 space-y-2 text-gray-600 bg-white border border-gray-100 rounded-md shadow-md dark:text-gray-300 dark:border-gray-700 dark:bg-gray-700"
                                    >
                                        <li class="flex">
                                            <a
                                                class="inline-flex items-center justify-between w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
                                                href="#"
                                            >
                                                <span>Messages</span>
                                                <span
                                                    class="inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-red-600 bg-red-100 rounded-full dark:text-red-100 dark:bg-red-600"
                                                >
                          13
                        </span>
                                            </a>
                                        </li>
                                        <li class="flex">
                                            <a
                                                class="inline-flex items-center justify-between w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
                                                href="#"
                                            >
                                                <span>Sales</span>
                                                <span
                                                    class="inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-red-600 bg-red-100 rounded-full dark:text-red-100 dark:bg-red-600"
                                                >
                          2
                        </span>
                                            </a>
                                        </li>
                                        <li class="flex">
                                            <a
                                                class="inline-flex items-center justify-between w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
                                                href="#"
                                            >
                                                <span>Alerts</span>
                                            </a>
                                        </li>
                                    </ul>
                                </Transition>


                            </template>
                        </li>
                        <!-- Profile menu -->
                        <li class="relative">
                            <button
                                class="align-middle rounded-full focus:shadow-outline-blue focus:outline-none"
                                @click="toggleProfileMenu"
                                @keydown.esc="closeProfileMenu"
                                v-click-outside="closeProfileMenu"
                                aria-label="Account"
                                aria-haspopup="true"
                            >
                                <img
                                    class="object-cover w-8 h-8 rounded-full"
                                    src="https://images.unsplash.com/photo-1502378735452-bc7d86632805?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=200&fit=max&s=aa3a807e1bbdfd4364d1f449eaa96d82"
                                    alt=""
                                    aria-hidden="true"
                                />
                            </button>
                            <template v-if="isProfileMenuOpen">
                                <Transition
                                    leave-active-class="transition ease-in duration-150"
                                    leave-from-class="opacity-100"
                                    leave-to-class="opacity-0"
                                >
                                    <ul

                                        @click.away="closeProfileMenu"
                                        @keydown.esc="closeProfileMenu"
                                        class="absolute right-0 w-56 p-2 mt-2 space-y-2 text-gray-600 bg-white border border-gray-100 rounded-md shadow-md dark:border-gray-700 dark:text-gray-300 dark:bg-gray-700"
                                        aria-label="submenu"
                                    >
                                        <li class="flex">
                                            <a
                                                class="inline-flex items-center w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
                                                href="#"
                                            >
                                                <svg
                                                    class="w-4 h-4 mr-3"
                                                    aria-hidden="true"
                                                    fill="none"
                                                    stroke-linecap="round"
                                                    stroke-linejoin="round"
                                                    stroke-width="2"
                                                    viewBox="0 0 24 24"
                                                    stroke="currentColor"
                                                >
                                                    <path
                                                        d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
                                                    ></path>
                                                </svg>
                                                <span>Profile</span>
                                            </a>
                                        </li>
                                        <li class="flex">
                                            <a
                                                class="inline-flex items-center w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
                                                href="#"
                                            >
                                                <svg
                                                    class="w-4 h-4 mr-3"
                                                    aria-hidden="true"
                                                    fill="none"
                                                    stroke-linecap="round"
                                                    stroke-linejoin="round"
                                                    stroke-width="2"
                                                    viewBox="0 0 24 24"
                                                    stroke="currentColor"
                                                >
                                                    <path
                                                        d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"
                                                    ></path>
                                                    <path d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                                </svg>
                                                <span>Settings</span>
                                            </a>
                                        </li>
                                        <li class="flex">
                                            <a
                                                class="inline-flex items-center w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
                                                href="#"
                                            >
                                                <svg
                                                    class="w-4 h-4 mr-3"
                                                    aria-hidden="true"
                                                    fill="none"
                                                    stroke-linecap="round"
                                                    stroke-linejoin="round"
                                                    stroke-width="2"
                                                    viewBox="0 0 24 24"
                                                    stroke="currentColor"
                                                >
                                                    <path
                                                        d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"
                                                    ></path>
                                                </svg>
                                                <span>Log out</span>
                                            </a>
                                        </li>
                                    </ul>
                                </Transition>

                            </template>
                        </li>
                    </ul>
                </div>
            </header>
            <main class="min-h-screen overflow-y-scroll mb-10">
                <slot></slot>
            </main>
        </div>
    </div>
</template>
