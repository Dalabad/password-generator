<template>
    <tr class="border-b border-gray-300 dark:border-gray-600">
        <td class="py-3 text-left font-medium text-gray-700 dark:text-gray-300">{{ label }}</td>
        <td class="py-3 text-right">
            <input type="checkbox" :checked="modelValue" @change="updateValue"
                class="form-checkbox h-5 w-5 text-blue-600" />
        </td>
    </tr>
</template>

<script setup>
const props = defineProps({
    label: {
        type: String,
        required: true,
    },
    modelValue: {
        type: Boolean,
        required: true,
    },
});

const emit = defineEmits();

const updateValue = (event) => {
    emit('update:modelValue', event.target.checked);
};
</script>
