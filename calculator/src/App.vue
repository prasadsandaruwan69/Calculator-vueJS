<template>
  <div class="min-h-screen bg-blue-100 flex flex-col items-center justify-center p-4">
    <!-- Responsive Navigation Bar -->
    <nav class="bg-white shadow-lg w-full fixed top-0 z-50">
      <div class="max-w-4xl mx-auto px-4">
        <div class="flex justify-between items-center h-16">
          <h1 class="text-xl font-bold text-gray-700">Pastel Calculator</h1>
          <button @click="toggleMenu" class="lg:hidden text-gray-600 text-2xl">
            ☰
          </button>
          <div class="hidden lg:flex space-x-4">
            <a href="#" class="nav-link">Home</a>
            <a href="#" class="nav-link">About</a>
            <a href="#" class="nav-link">Contact</a>
          </div>
        </div>
      </div>
      <div v-if="isMenuOpen" class="lg:hidden flex flex-col space-y-2 bg-white p-4 shadow-md">
        <a href="#" class="nav-link">Home</a>
        <a href="#" class="nav-link">About</a>
        <a href="#" class="nav-link">Contact</a>
      </div>
    </nav>

    <!-- Calculator -->
    <div class="w-full max-w-sm bg-white p-4 rounded-xl shadow-lg mt-20">
      <!-- Display Screen -->
      <div class="mb-4">
        <input 
          v-model="inputStr"
          type="text" 
          class="w-full p-3 text-xl font-semibold border border-gray-300 rounded-md focus:outline-none text-right bg-gray-50"
          readonly
        />
      </div>

      <!-- Grid Buttons -->
      <div class="grid grid-cols-4 gap-2">
        <button @click="memoryRecall()" class="btn pastel-pink">MRC</button>
        <button @click="memorySubtract()" class="btn pastel-pink">M-</button>
        <button @click="memoryAdd()" class="btn pastel-pink">M+</button>
        <button @click="updateDisplay('%')" class="btn pastel-pink">%</button>

        <button @click="backspace()" class="btn pastel-yellow">←</button>
        <button @click="updateDisplay('7')" class="btn pastel-yellow">7</button>
        <button @click="updateDisplay('8')" class="btn pastel-yellow">8</button>
        <button @click="updateDisplay('9')" class="btn pastel-yellow">9</button>

        <button @click="clearEntry()" class="btn pastel-orange">CE</button>
        <button @click="updateDisplay('4')" class="btn pastel-green">4</button>
        <button @click="updateDisplay('5')" class="btn pastel-green">5</button>
        <button @click="updateDisplay('6')" class="btn pastel-green">6</button>

        <button @click="clearAll()" class="btn pastel-orange">AC</button>
        <button @click="updateDisplay('1')" class="btn pastel-purple">1</button>
        <button @click="updateDisplay('2')" class="btn pastel-purple">2</button>
        <button @click="updateDisplay('3')" class="btn pastel-purple">3</button>

        <button @click="updateDisplay('0')" class="btn pastel-white">0</button>
        <button @click="updateDisplay('00')" class="btn pastel-white">00</button>
        <button @click="updateDisplay('.')" class="btn pastel-white">.</button>
        <button @click="calculate()" class="btn pastel-purple">=</button>

        <button @click="updateDisplay('+')" class="btn pastel-pink">+</button>
        <button @click="updateDisplay('-')" class="btn pastel-pink">-</button>
        <button @click="updateDisplay('*')" class="btn pastel-pink">×</button>
        <button @click="updateDisplay('/')" class="btn pastel-pink">÷</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      inputStr: "",
      memory: 0, // Memory storage for MRC, M+, M-
      isMenuOpen: false, // Mobile menu toggle state
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    updateDisplay(val) {
      this.inputStr += val;
    },
    clearEntry() {
      this.inputStr = this.inputStr.slice(0, -1);
    },
    clearAll() {
      this.inputStr = "";
    },
    backspace() {
      this.inputStr = this.inputStr.slice(0, -1);
    },
    calculate() {
      try {
        this.inputStr = Function(`'use strict'; return (${this.inputStr})`)();
      } catch (e) {
        this.inputStr = "Error";
      }
    },
    // Memory Functions
    memoryAdd() {
      this.memory += parseFloat(this.inputStr) || 0;
    },
    memorySubtract() {
      this.memory -= parseFloat(this.inputStr) || 0;
    },
    memoryRecall() {
      this.inputStr += this.memory;
    },
  },
};
</script>

<style scoped>
/* General Button Styling */
.btn {
  @apply text-xl font-bold w-full h-16 rounded-full shadow-md transition-all;
}

/* Navbar Styles */
.nav-link {
  @apply block text-gray-700 hover:text-blue-500 transition;
}

/* Color Themes */
.pastel-pink { background-color: #f7cac9; }
.pastel-yellow { background-color: #f9e79f; }
.pastel-orange { background-color: #f4a261; }
.pastel-green { background-color: #c5e1a5; }
.pastel-purple { background-color: #d5a6bd; }
.pastel-white { background-color: #fdfdfd; }
</style>
