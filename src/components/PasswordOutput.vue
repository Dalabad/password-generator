<template>
    <div class="relative mb-4">
        <input v-model="internalValue" type="text" placeholder="Generated Password"
            class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg shadow-sm focus:ring focus:ring-indigo-200 focus:ring-opacity-50 focus:outline-none bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-200"
            readonly />
        <button @click="copyToClipboard"
            class="absolute inset-y-0 right-0 flex items-center pr-3 text-gray-500 hover:text-gray-700 dark:text-gray-400 hover:dark:text-gray-200">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round"
                    d="M15.75 17.25v3.375c0 .621-.504 1.125-1.125 1.125h-9.75a1.125 1.125 0 0 1-1.125-1.125V7.875c0-.621.504-1.125 1.125-1.125H6.75a9.06 9.06 0 0 1 1.5.124m7.5 10.376h3.375c.621 0 1.125-.504 1.125-1.125V11.25c0-4.46-3.243-8.161-7.5-8.876a9.06 9.06 0 0 0-1.5-.124H9.375c-.621 0-1.125.504-1.125 1.125v3.5m7.5 10.375H9.375a1.125 1.125 0 0 1-1.125-1.125v-9.25m12 6.625v-1.875a3.375 3.375 0 0 0-3.375-3.375h-1.5a1.125 1.125 0 0 1-1.125-1.125v-1.5a3.375 3.375 0 0 0-3.375-3.375H9.75" />
            </svg>
        </button>
    </div>
</template>

<script setup>
import { ref, defineProps, watch } from 'vue';

const props = defineProps({
    useLetters: Boolean,
    useNumbers: Boolean,
    useSpecialCharacters: Boolean,
    avoidAmbiguousCharacters: Boolean,
    passwordLength: Number,
    regeneratePassword: Number,
});

// Local state to hold the password
const internalValue = ref('');

// Function to get 25% of special characters randomly
const getRandomSpecialCharacters = (characters, percentage) => {
    const numCharactersToSelect = Math.floor(characters.length * percentage);
    const shuffled = characters.split('').sort(() => 0.5 - Math.random());
    return shuffled.slice(0, numCharactersToSelect).join('');
};

// Verify if a password confirms to the expected rules
const checkPasswordValidity = (password) => {
    const hasLetters = props.useLetters ? /[a-zA-Z]/.test(password) : true;
    const hasNumbers = props.useNumbers ? /[0-9]/.test(password) : true;
    const hasSpecialChars = props.useSpecialCharacters ? /[!@#$%^&*()-_=+[\]{}|;:'",.<>?/~`]/.test(password) : true;

    return hasLetters && hasNumbers && hasSpecialChars;
};

// Function to generate password
const generatePassword = () => {
    let availableCharacters = '';

    // Define character sets
    const letters = 'abcdefghijklmnopqrstuvwxyz';
    const numbers = '0123456789';
    const specialCharacters = '!@#$%^&*()-_=+[]{}|;:\'",.<>?/~`';
    const ambiguousCharacters = 'il1Lo0O';

    // Build the available characters based on user settings
    if (props.useLetters) {
        availableCharacters += letters;
    }
    if (props.useNumbers) {
        availableCharacters += numbers;
    }
    if (props.useSpecialCharacters) {
        availableCharacters += getRandomSpecialCharacters(specialCharacters, 0.25);
    }
    if (props.avoidAmbiguousCharacters) {
        availableCharacters = availableCharacters.split('').filter(c => !ambiguousCharacters.includes(c)).join('');
    }

    // Generate password
    if (availableCharacters.length > 0) {
        internalValue.value = Array.from({ length: props.passwordLength }, () =>
            availableCharacters.charAt(Math.floor(Math.random() * availableCharacters.length))
        ).join('');
    } else {
        internalValue.value = ''; // No characters available
    }

    // If password does not align with rules, generate a new one
    if (checkPasswordValidity(internalValue.value) === false) {
        generatePassword();
    }
};

// Expose a method to regenerate passwords
const regenerate = () => {
    generatePassword();
};

// Watch for changes in props and regenerate password if any prop changes
watch(
    () => [props.useLetters, props.useNumbers, props.useSpecialCharacters, props.avoidAmbiguousCharacters, props.passwordLength, props.regeneratePassword],
    () => {
        generatePassword();
    },
    { immediate: true } // Run immediately on component mount
);

// Copy text to clipboard
const copyToClipboard = () => {
    navigator.clipboard.writeText(internalValue.value);
};
</script>

<style scoped></style>
