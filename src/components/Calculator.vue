<template>
  <div class="calculator">
    <input type="text" v-model="display" readonly>
    <div class="buttons">
      <button v-for="(button,index) in buttons" :key="index" @click="handleClick(button)">
        {{ Array.isArray(button)?button.join(''):button }}
      </button>
      <button class="clear-button" @click="clear">Clear</button>
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
      'MC', 'M+', 'M-', 'MR',  
      '7', '8', '9', 'MS',
      '4', '5', '6', '÷',
      '1', '2', '3', 'x',
      '0', '.', '+', '-',
      '%',"=",
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
            
            this.display += '*';
    },
    '÷': () => {
            this.display += '/';
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
    'clear': () => {
      this.display = '';
    },
  };

  if (map[button]) {
    map[button]();
  } else if (button === '=') {
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
  gap: 10px;
}

button {
  width: 100%;
  height: 50px;
  background-color: #f1f1f1;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #ccc;
}

.clear-button {
  grid-column: span 2;
  background-color: #f44336;
  color: white;
}

.clear-button:hover {
  background-color: #d32f2f;
}
</style>
