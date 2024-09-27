<template>
    <tr class="border-b border-gray-300 dark:border-gray-600">
        <td class="py-3 text-left font-medium text-gray-700 dark:text-gray-300">{{ label }}</td>
        <td class="py-3 text-right">
            <input type="range" v-model="internalValue" @input="updateValue" min="8" max="50"
                class="form-range w-full" />
            <p class="text-right text-sm text-gray-600 dark:text-gray-400">{{ internalValue }}</p>
        </td>
    </tr>
</template>

<script setup>
import { ref, watch, defineProps, defineEmits } from 'vue';

const props = defineProps({
    label: {
        type: String,
        required: true,
    },
    modelValue: {
        type: Number,
        required: true,
    },
});

const emit = defineEmits();

const internalValue = ref(props.modelValue);

watch(() => props.modelValue, (newValue) => {
    internalValue.value = newValue;
});

const updateValue = () => {
    emit('update:modelValue', internalValue.value);
};
</script>

<style scoped>
input[type="range"] {
    accent-color: #3b82f6;
}
</style>