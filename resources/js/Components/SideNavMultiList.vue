<script setup>
import {ref} from 'vue';

let isPagesMenuOpen = ref(false);
import {ChevronRightIcon, ChevronDownIcon} from '@heroicons/vue/solid';

defineProps({
    active: {
        type: Boolean,
        default: false,
    },
    name: {
        type: String,
        default: "",
    },

});


let togglePagesMenu = () => {
    isPagesMenuOpen.value = !isPagesMenuOpen.value;
};
</script>


<template>
    <li class="relative px-6 py-3">
        <span v-if="active" class="absolute inset-y-0 left-0 w-1 h-14 bg-blue-600"></span>

        <button
            class="inline-flex items-center justify-between w-full text-sm font-semibold transition-colors duration-150 hover:text-gray-50 dark:hover:text-gray-200 dark:text-gray-100"
            @click="togglePagesMenu"
            aria-haspopup="true">
                <span class="inline-flex items-center">
                  <slot name="trailingIcon"></slot>
                  <span class="ml-4">{{ name }}</span>
                </span>
            <ChevronDownIcon v-if="isPagesMenuOpen" class="h-4 w-4"/>
            <ChevronRightIcon v-else class="h-4 w-4"/>

        </button>
        <template v-if="isPagesMenuOpen">
            <Transition
                enter-active-class="transition-all ease-in-out duration-300"
                enter-from-class="opacity-25 max-h-0"
                enter-to-class="opacity-100 max-h-xl"
                leave-active-class="transition-all ease-in-out duration-300"
                leave-from-class="opacity-100 max-h-xl"
                leave-to-class="opacity-0 max-h-0">
                <ul class="p-2 mt-2 space-y-2 overflow-hidden text-sm font-medium text-gray-500 rounded-none border-t border-t-gray-700 dark:text-gray-400 dark:bg-gray-900 "
                    aria-label="submenu">
                    <slot></slot>
                </ul>
            </Transition>

        </template>
    </li>
</template>




