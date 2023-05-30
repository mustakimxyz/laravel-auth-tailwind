<script setup lang="ts">
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
</script>

<template>
    <div
        class="min-h-screen flex flex-col sm:justify-center items-center bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500"
    >
        <div class="w-full sm:max-w-lg mt-8 px-8 py-6 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-600 sm:rounded-lg">
            <slot />
        </div>
    </div>
</template>
