<template>
    <div class="text-white py-4">
        <div class="flex justify-center items-center">
            <span class="text-sm flex items-center space-x-1">
                <span>&copy; {{ currentYear }}</span>
                <a href="https://github.com/Dalabad/password-generator" class="flex items-center hover:text-blue-400">
                    Dalabad
                </a>
            </span>
        </div>
    </div>
</template>

<script setup>
const currentYear = new Date().getFullYear(); // Get the current year
</script>

<style scoped>
</style>
