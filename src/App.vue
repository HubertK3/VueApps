<template>
  <div class="upper-container">
    <div class="timer">{{ timeLeft }}</div>
    <Custom-Button></Custom-Button>
  </div>
  <div id="app" class="page">
    <div class="calculator">
      <div class="result-window">{{ resultWindow }}</div>
      <div class="display">{{ display }}</div>
      <div class="buttons">
        <button v-for="button in buttons" :key="button" @click="handleButtonClick(button)">{{ button }}</button>
        <button @click="clearDisplay">C</button>
      </div>
    </div>
  </div>
</template>

<script>
import CustomButton from './CustomButton.vue';

export default {
  components: {
    CustomButton,
  },
  data() {
    return {
      display: "",
      resultWindow: "",
      buttons: ['1', '2', '3', '+', '4', '5', '6', '-', '7', '8', '9', '*', '0', '%', '/', '='],
      timer: null,
      timeLeft: '10:00',
    };
  },
  mounted() {
    this.startTimer();
  },
  methods: {
    handleButtonClick(button) {
      if (button === '=') {
        this.calculateResult();
      } else if (button === '%') {
        this.calculatePercentage();
      } else {
        this.appendToDisplay(button);
      }
    },
    appendToDisplay(value) {
      this.display += value;
    },
    calculatePercentage() {
      if (this.display !== "") {
        this.display = String(parseFloat(this.display) / 100);
      }
    },
    clearDisplay() {
      this.display = "";
      this.resultWindow = "";
    },
    calculateResult() {
      try {
        const result = new Function('return ' + this.display)();
        if (result === Infinity || isNaN(result)) {
          this.resultWindow = "Nie dziel przez 0";
        } else {
          this.resultWindow = this.display + " = " + result;
          this.display = result.toString();
        }
      } catch (error) {
        this.resultWindow = "Błąd";
      }
    },
    startTimer() {
      let time = 600;
      this.timer = setInterval(() => {
        if (time > 0) {
          time--;
          this.timeLeft = `${Math.floor(time / 60)}:${('0' + time % 60).slice(-2)}`;
        } else {
          clearInterval(this.timer);
          if (confirm('Czas upłynął! Czy zresetować timer?')) {
            this.resetTimer();
          }
        }
      }, 1000);
    },
    resetTimer() {
      clearInterval(this.timer);
      this.timer = null;
      this.timeLeft = '10:00';
      this.startTimer();
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
.timer {
  font-size: 20px;
  color: rgb(21, 21, 21);
}
.upper-container {
  text-align: left;
  margin-bottom: 0px;
}
</style>

