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
      const map = {
        '+': () => {
            this.display += '+';
        },
        '-': () => {
            this.display += '-';
        },
        'x': () => {
            this.display += 'x';
        },
        '÷': () => {
            this.display += '÷';
        },
        'MC': () => {
          this.memory = null;
        },
        'M+': () => {
          if (this.display !== '') {
            this.memory = (parseFloat(this.memory) || 0) + parseFloat(this.display);
          }
        },
        'M-': () => {
          if (this.display !== '') {
            this.memory = (parseFloat(this.memory) || 0) - parseFloat(this.display);
          }
        },
        'MR': () => {
          if (this.memory !== null) {
            this.display += this.memory.toString();
          }
        },
        'MS': () => {
          this.memory = parseFloat(this.display);
        },
      };
      if (map[button]) {
        map[button].bind(this)();
      }

      if (button === '=') {
        this.calculate();
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
    memoryClear() {
      this.memory = null;
    },
    memoryAddition() {
      if (this.display !== '') {
        this.memory = (parseFloat(this.memory) || 0) + parseFloat(this.display);
      }
    },
    memorySubtraction() {
      if (this.display !== '') {
        this.memory = (parseFloat(this.memory) || 0) - parseFloat(this.display);
      }
    },
    memoryDisplay() {
      if (this.memory !== null) {
        this.display += this.memory.toString();
      }
    },
    memorySave() {
      this.memory = parseFloat(this.display);
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
