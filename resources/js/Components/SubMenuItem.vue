<template>
    <li
        class=" py-1 transition-colors duration-150 hover:text-gray-50 dark:hover:text-gray-200 dark:text-gray-100">
        <a class="w-full flex items-center" :href="href">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"  class="bi bi-dot h-6 w-6" viewBox="0 0 16 16">
                <path d="M8 9.5a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3z"/>
            </svg>
            <slot></slot>
        </a>
    </li>
</template>

<script setup>

defineProps({
    href: {
        type: String,
        default: "#",
    },
});

</script>

<style scoped>

</style>
