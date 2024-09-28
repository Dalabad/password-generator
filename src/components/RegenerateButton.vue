<template>
    <div class="flex justify-center m-6">
        <button @click="regenerate"
            class="px-4 py-2 bg-blue-600 text-white rounded-lg shadow hover:bg-blue-700 focus:outline-none focus:ring focus:ring-blue-200">
            Regenerate Passwords
        </button>
    </div>
</template>

<script setup>
const emit = defineEmits();

// Emit an event to regenerate passwords
const regenerate = () => {
    emit('regenerate-passwords');
};
</script>

<style scoped></style>
