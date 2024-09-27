<template>
    <tr class="border-b border-gray-300 dark:border-gray-600">
        <td class="py-3 text-left font-medium text-gray-700 dark:text-gray-300">{{ label }}</td>
        <td class="py-3 text-right">
            <select v-model="selectedValue" @change="updateValue"
                class="px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg shadow-sm focus:ring focus:ring-indigo-200 focus:ring-opacity-50 focus:outline-none bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-200">
                <option v-for="value in parsedValues" :key="value" :value="value">{{ value }}</option>
            </select>
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
    values: {
        type: String,
        required: true,
    },
    modelValue: {
        type: Number,
        required: true,
    },
});

const emit = defineEmits();

// Initialize parsedValues and selectedValue based on the props
const parsedValues = ref(props.values.split(','));
const selectedValue = ref(props.modelValue);

// Watch for changes in the values prop and update parsedValues accordingly
watch(() => props.values, (newValues) => {
    parsedValues.value = newValues.split(',');
    selectedValue.value = parsedValues.value[0]; // Reset selected value if options change
});

// Watch for changes in modelValue and update selectedValue
watch(() => props.modelValue, (newValue) => {
    selectedValue.value = newValue;
});

// Emit the new value when selection changes
const updateValue = () => {
    emit('update:modelValue', selectedValue.value);
};
</script>

<style scoped>
</style>
