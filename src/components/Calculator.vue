<template>
  <div class="calculator">
    <input type="text" v-model="display" readonly>
    <div class="buttons">
      <button v-for="button in buttons" :key="button" @click="handleClick(button)">
        {{ button }}
      </button>
      <button class="clear-button" @click="clear">Clear</button>
      <button class="memory-button" @click="memoryClear">MC</button>
      <button class="memory-button" @click="memoryAddition">M+</button>
      <button class="memory-button" @click="memorySubtraction">M-</button>
      <button class="memory-button" @click="memoryDisplay">MR</button>
      <button class="memory-button" @click="memorySave">MS</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorComponent',
  data() {
    return {
      display: '',
      memory: null,
      buttons: [
        '7', '8', '9', '÷',
        '4', '5', '6', 'x',
        '1', '2', '3', '-',
        '0', '.', '+', '=', '%',
      ]
    };
  },
  methods: {
    handleClick(button) {
      if (button === '=') {
        this.calculate();
      } else if (button === '+') {
        this.addition();
      } else if (button === '-') {
        this.subtraction();
      } else if (button === 'x') {
        this.multiplication();
      } else if (button === '÷') {
        this.division();
      } else if (button === '%') {
        this.percentage();
      } else if (button === 'MC') {
        this.memoryClear();
      } else if (button === 'M+') {
        this.memoryAddition();
      } else if (button === 'M-') {
        this.memorySubtraction();
      } else if (button === 'MR') {
        this.memoryDisplay();
      } else if (button === 'MS') {
        this.memorySave();
      } else if (button === '.') {
        if (this.display.includes('.')) {
          return;
        } else if (this.display === '' && (button === '÷' || button === 'x' || button === '-' || button === '+' || button === '%')) {
          return;
        } this.display += button;
      } else {
        this.display += button;
      }
    },
 
    calculate() {
      try {
        const result = new Function(`return ${this.display}`)();
        this.display = result.toString();
      } catch (error) {
        this.display = 'Error';
      }
    },
    clear() {
      this.display = '';
    },
    addition() {
      try {
        const result = new Function(`return ${this.display}`)();
        this.display = result.toString();
      } catch (error) {
        this.display = 'Error';
      }
    },
    subtraction() {
      try {
        const result = new Function(`return ${this.display}`)();
        this.display = result.toString();
      } catch (error) {
        this.display = 'Error';
      }
    },
    multiplication() {
      try {
        const result = new Function(`return ${this.display.replace('x', '*')}`)();
        this.display = result.toString();
      } catch (error) {
        this.display = 'Error';
      }
    },
    division() {
      try {
        const result = new Function(`return ${this.display.replace('÷', '/')}`)();
        this.display = result.toString();
      } catch (error) {
        this.display = 'Error';
      }
    },
    percentage() {
      this.display = (parseFloat(this.display) / 100).toString();
    },
    memoryClear() {
      this.memory = null;
    },
    memoryAddition() {
      if (this.display !== '') {
        this.memory = this.display;
      }
    },
    memorySubtraction() {
      if (this.display !== null) {
        let memoryValue = parseFloat(this.memory);
        let substValue = parseFloat(this.display);
        this.memory = (memoryValue - substValue).toString();
      }
    },
    memoryDisplay() {
      if (this.memory !== null) {
        this.display += this.memory;
      }
    },
    memorySave() {
      this.memory = this.display;
    },
  },
};
</script>

<style scoped>
.calculator {
  width: 300px;
  margin: 0 auto;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
}

input {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  font-size: 18px;
  text-align: right;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 5px;
}

button {
  width: 100%;
  height: 40px;
  background-color: #eee;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #ccc;
}

.clear-button {
  background-color: #f44336;
  color: white;
}

.clear-button:hover {
  background-color: #d32f2f;
}
</style>
