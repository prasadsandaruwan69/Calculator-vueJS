<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-blue-100 p-4">
    <div class="w-full max-w-sm bg-white p-4 rounded-xl shadow-lg">
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
        <!-- Memory Buttons -->
        <button @click="memoryRecall()" class="btn pastel-pink">MRC</button>
        <button @click="memorySubtract()" class="btn pastel-pink">M-</button>
        <button @click="memoryAdd()" class="btn pastel-pink">M+</button>
        <button @click="updateDisplay('%')" class="btn pastel-pink">%</button>

        <!-- Row 2 -->
        <button @click="backspace()" class="btn pastel-yellow">←</button>
        <button @click="updateDisplay('7')" class="btn pastel-yellow">7</button>
        <button @click="updateDisplay('8')" class="btn pastel-yellow">8</button>
        <button @click="updateDisplay('9')" class="btn pastel-yellow">9</button>

        <!-- Row 3 -->
        <button @click="clearEntry()" class="btn pastel-orange">CE</button>
        <button @click="updateDisplay('4')" class="btn pastel-green">4</button>
        <button @click="updateDisplay('5')" class="btn pastel-green">5</button>
        <button @click="updateDisplay('6')" class="btn pastel-green">6</button>

        <!-- Row 4 -->
        <button @click="clearAll()" class="btn pastel-orange">AC</button>
        <button @click="updateDisplay('1')" class="btn pastel-purple">1</button>
        <button @click="updateDisplay('2')" class="btn pastel-purple">2</button>
        <button @click="updateDisplay('3')" class="btn pastel-purple">3</button>

        <!-- Row 5 -->
        <button @click="updateDisplay('0')" class="btn pastel-white">0</button>
        <button @click="updateDisplay('00')" class="btn pastel-white">00</button>
        <button @click="updateDisplay('.')" class="btn pastel-white">.</button>
        <button @click="calculate()" class="btn pastel-purple">=</button>

        <!-- Row 6 (Operators) -->
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
      memory: 0, // For memory functions
    };
  },
  methods: {
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

/* Color Themes */
.pastel-pink { background-color: #f7cac9; }
.pastel-yellow { background-color: #f9e79f; }
.pastel-orange { background-color: #f4a261; }
.pastel-green { background-color: #c5e1a5; }
.pastel-purple { background-color: #d5a6bd; }
.pastel-white { background-color: #fdfdfd; }
</style>
