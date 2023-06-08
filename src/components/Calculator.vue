<template>
    <div class="calculator">
      <input type="text" v-model="display" readonly>
      <div class="buttons">
        <button v-for="button in buttons" :key="button" @click="handleClick(button)">
          {{ button }}
        </button>
        <button @click="clear">Clear</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CalculatorComponent',
    data() {
      return {
        display: '',
        buttons: [
          '7', '8', '9', '÷',
          '4', '5', '6', '×',
          '1', '2', '3', '-',
          '0', '.', '+', '='
        ]
      };
    },
    methods: {
      handleClick(button) {
        if (button === '=') {
          this.calculate();
        } else if (button === 'Clear') {
          this.clear();
        } else {
          this.display += button;
        }
      },
      calculate() {
        try {
          this.display = eval(this.display.replace('×', '*').replace('÷', '/'));
        } catch (error) {
          this.display = 'Error';
        }
      },
      clear() {
        this.display = '';
      }
    }
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
  }
  
  button:hover {
    background-color: #ccc;
  }
  </style>
  