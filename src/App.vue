<template>
  <div
    class="min-h-screen flex items-center justify-center bg-gray-100 dark:bg-gray-800 p-6 text-gray-800 dark:text-gray-200">
    <div class="bg-white dark:bg-gray-700 shadow-lg rounded-lg p-6 w-full max-w-md">
      <h2 class="text-2xl font-semibold mb-6 text-gray-800 dark:text-gray-200 flex justify-center items-center">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
          class="size-6 mr-2">
          <path stroke-linecap="round" stroke-linejoin="round"
            d="M9 12.75 11.25 15 15 9.75m-3-7.036A11.959 11.959 0 0 1 3.598 6 11.99 11.99 0 0 0 3 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285Z" />
        </svg>
        Generate Secure Password
      </h2>


      <table class="w-full mb-6">
        <tbody>
          <CheckboxRow label="Use letters [a-z]" v-model="useLetters" />
          <CheckboxRow label="Use numbers [0-9]" v-model="useNumbers" />
          <CheckboxRow label="Use Special Characters" v-model="useSpecialCharacters" />
          <CheckboxRow label="Avoid Ambiguous Characters" v-model="avoidAmbiguousCharacters" />
          <RangeRow label="Password length" v-model.number="passwordLength" />
          <SelectRow label="Amount of Passwords" values="1,5,10,25" v-model.number="passwordAmount" />
        </tbody>
      </table>

      <RegenerateButton @regenerate-passwords="updatePasswords" />

      <div v-for="(password, index) in passwordAmount" :key="index">
        <PasswordOutput :useLetters="useLetters" :useNumbers="useNumbers" :useSpecialCharacters="useSpecialCharacters"
          :avoidAmbiguousCharacters="avoidAmbiguousCharacters" :passwordLength="passwordLength"
          :regeneratePassword="regeneratePassword" />
      </div>

      <Footer />
    </div>
  </div>
</template>

<script setup>
// Import the components
import CheckboxRow from './components/CheckboxRow.vue';
import RangeRow from './components/RangeRow.vue';
import SelectRow from './components/SelectRow.vue';
import RegenerateButton from './components/RegenerateButton.vue';
import PasswordOutput from './components/PasswordOutput.vue';
import Footer from './components/Footer.vue'

// Your reactive properties and methods
import { ref, onMounted } from 'vue';

const useLetters = ref(true);
const useNumbers = ref(true);
const useSpecialCharacters = ref(true);
const avoidAmbiguousCharacters = ref(true);
const passwordLength = ref(20);
const passwordAmount = ref(5);
const regeneratePassword = ref(null)

function updatePasswords() {
  regeneratePassword.value = Date.now()
}

// Force dark mode as default on page load
onMounted(() => {
  document.documentElement.classList.add('dark');
});
</script>

<style scoped></style>
