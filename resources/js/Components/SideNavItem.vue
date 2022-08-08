<template>
    <li class="relative px-6 py-3 ">
        <span v-if="active" class="absolute inset-y-0 left-0 w-1 bg-blue-600"></span>
        <a
            class="inline-flex items-center w-full text-sm font-semibold transition-colors duration-150 hover:text-gray-50 dark:hover:text-gray-200 dark:text-gray-100"
            :href="href">
            <slot></slot>
            <span class="ml-4">{{ name }}</span>
        </a>
    </li>
</template>

<script setup>

defineProps({
    href: {
        type: String,
        default: '#',
    },
    name: {
        type: String,
        default: "",
    },
    active: {
        type: Boolean,
        default: false,
    },
});
</script>

<style scoped>

</style>
