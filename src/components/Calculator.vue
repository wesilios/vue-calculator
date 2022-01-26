<template>
  <div class="calculator">
    <div class="display">
      <div class="sup">{{ calculator.previous }}</div>
      <div class="sup">{{ calculator.operator }}</div>
      <div class="current">{{ calculator.current || '0' }}</div>
    </div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="setOperator('÷')">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="setOperator('x')">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="setOperator('-')">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="setOperator('+')">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script lang="ts">
import {defineComponent} from 'vue'

interface CalculatorData {
  previous: string,
  current: string,
  operator: string,
  operatorClicked: boolean
}

export default defineComponent({
  name: 'Calculator',
  props: {
    msg: String
  },
  data: function () {
    return {
      count: 0,
      calculator: {
        previous: '',
        current: '',
        operator: '',
        operatorClicked: false,
      } as CalculatorData
    }
  },
  methods: {
    clear: function (): void {
      this.calculator.current = '0'
    },
    sign: function (): void {
      if (this.calculator.current !== '0') {
        this.calculator.current = this.calculator.current.charAt(0) === '-' ? this.calculator.current.slice(1) : `-${this.calculator.current}`;
      }
    },
    percent: function (): void {
      this.calculator.current = `${parseFloat(this.calculator.current) / 100}`;
    },
    append: function (number: string): void {
      this.calculator.current = `${this.calculator.current === '0' ? '' : this.calculator.current}${number}`;
    },
    dot: function (): void {
      if (this.calculator.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setOperator: function (operator: string): void {
      this.calculator.operator = operator;
      this.calculator.operatorClicked = true;
      this.calculator.previous = this.calculator.current;
      this.clear();
    },
    divides: (a: number, b: number) => a / b,
    times: (a: number, b: number) => a * b,
    minus: (a: number, b: number) => a - b,
    add: (a: number, b: number) => a + b,
    equal: function (): void {
      switch (this.calculator.operator) {
        case '÷':
          this.calculator.current = `${this.divides(parseFloat(this.calculator.previous), parseFloat(this.calculator.current))}`;
          break;
        case 'x':
          this.calculator.current = `${this.times(parseFloat(this.calculator.previous), parseFloat(this.calculator.current))}`;
          break;
        case '-':
          this.calculator.current = `${this.minus(parseFloat(this.calculator.previous), parseFloat(this.calculator.current))}`;
          break;
        case '+':
          this.calculator.current = `${this.add(parseFloat(this.calculator.previous), parseFloat(this.calculator.current))}`;
          break;
      }
      this.calculator.previous = '';
      this.calculator.operator = '';
    }
  }
})
</script>

<style scoped>
.calculator {
  font-size: 35px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  max-width: 400px;
  margin: 0 auto;
}

.display {
  grid-column: 1/5;
  background-color: rgba(3, 7, 14, 0.9);
  color: #ffffff;
  text-align: right;
  padding: 5px 20px;
}

.display .sup {
  padding: 0 5px;
  height: 20px;
  font-size: 20px;
}

.btn {
  background-color: #eee;
  border: 1px solid #333;
  padding: 10px 10px;
  cursor: pointer;
  font-size: 25px;
}

.zero {
  grid-column: 1/3;
}

.operator {
  background-color: orange;
  color: #ffffff;
}
</style>
