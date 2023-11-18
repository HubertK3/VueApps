<template>
  <div id="app" class="page">
    <div class="calculator">
      <div class="result-window">{{ resultWindow }}</div>
      <div class="display">{{ display }}</div>
      <div class="buttons">
        <button @click="appendToDisplay('1')">1</button>
        <button @click="appendToDisplay('2')">2</button>
        <button @click="appendToDisplay('3')">3</button>
        <button @click="appendToDisplay('+')">+</button>
        <button @click="appendToDisplay('4')">4</button>
        <button @click="appendToDisplay('5')">5</button>
        <button @click="appendToDisplay('6')">6</button>
        <button @click="appendToDisplay('-')">-</button>
        <button @click="appendToDisplay('7')">7</button>
        <button @click="appendToDisplay('8')">8</button>
        <button @click="appendToDisplay('9')">9</button>
        <button @click="appendToDisplay('*')">*</button>
        <button @click="appendToDisplay('0')">0</button>
        <button @click="appendToDisplay('**')">^</button>
        <button @click="removeLastDigit">Back</button>
        <button @click="clearDisplay">C</button>
        <button @click="calculateResult">=</button>
        <button @click="appendToDisplay('/')">/</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: "",
      resultWindow: "",
    };
  },
  methods: {
    appendToDisplay(value) {
      this.display += value;
    },
    removeLastDigit() {
      this.display = this.display.slice(0, -1);
    },
    clearDisplay() {
      this.display = "";
      this.resultWindow = "";
    },
    calculateResult() {
      try {
        const result = eval(this.display);
        if (result === Infinity || isNaN(result)) {
          this.resultWindow = "Nie dziel przez 0";
        } else {
          this.resultWindow = this.display + " = " + result;
          this.display = result;
        }
      } catch (error) {
        this.resultWindow = "Błąd";
      }
    },
  },
};
</script>

<style>
.page {
  background-color: rgba(21, 21, 21, 0.55);
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.calculator {
  background-color: rgba(255, 98, 0, 0.22);
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  width: 300px;
}

.display {
  font-size: 24px;
  margin-bottom: 10px;
}

.buttons button {
  font-size: 18px;
  width: 60px;
  height: 60px;
  margin: 5px;
}
</style>

