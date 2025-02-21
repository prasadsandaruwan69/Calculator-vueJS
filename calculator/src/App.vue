<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4">
    <div class="w-full max-w-xs bg-white p-4 rounded-lg shadow-md">
      <div class="mb-4">
        <input 
          v-model="inputStr"
          type="text" 
          class="w-full p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-right"
          readonly
        />
      </div>

      <!-- Display Result -->
      <div class="text-right text-xl font-bold text-gray-700 mb-4">
        {{ result }}
      </div>

      <div class="grid grid-cols-4 gap-2">
        <button @click="updateDisplay('+')" class="btn">+</button>
        <button @click="updateDisplay('-')" class="btn">-</button>
        <button @click="updateDisplay('*')" class="btn">*</button>
        <button @click="updateDisplay('/')" class="btn">/</button>

        <button @click="updateDisplay('7')" class="btn">7</button>
        <button @click="updateDisplay('8')" class="btn">8</button>
        <button @click="updateDisplay('9')" class="btn">9</button>
        <button @click="clearDisplay()" class="btn">C</button>

        <button @click="updateDisplay('4')" class="btn">4</button>
        <button @click="updateDisplay('5')" class="btn">5</button>
        <button @click="updateDisplay('6')" class="btn">6</button>
        <button @click="calculate()" class="btn">=</button>

        <button @click="updateDisplay('1')" class="btn">1</button>
        <button @click="updateDisplay('2')" class="btn">2</button>
        <button @click="updateDisplay('3')" class="btn">3</button>
        <button @click="updateDisplay('0')" class="btn">0</button>
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
      result: "",
    };
  },
  methods: {
    updateDisplay(val) {
      this.inputStr += val;
    },
    clearDisplay() {
      this.inputStr = "";
      this.result = "";
    },
    calculate() {
      try {
        this.result = Function(`'use strict'; return (${this.inputStr})`)();
      } catch (e) {
        this.result = "Error";
      }
    },
  },
};
</script>

<style scoped>
.btn {
  @apply bg-blue-500 text-white p-3 rounded-lg shadow-md hover:bg-blue-600 transition-all;
}
</style>
