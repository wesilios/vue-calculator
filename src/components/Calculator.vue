<template>
  <div class="calculator">
    <div class="display">{{ current || '0' }}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn">%</div>
    <div class="btn operator">÷</div>
    <div class="btn">7</div>
    <div class="btn">8</div>
    <div class="btn">9</div>
    <div class="btn operator">x</div>
    <div class="btn">4</div>
    <div class="btn">5</div>
    <div class="btn">6</div>
    <div class="btn operator">-</div>
    <div class="btn">1</div>
    <div class="btn">2</div>
    <div class="btn">3</div>
    <div class="btn operator">+</div>
    <div class="btn zero">0</div>
    <div class="btn">.</div>
    <div class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props: {
    msg: String
  },
  data () {
    return {
      current: '123',
    }
  },
  methods: {
    clear () {
      this.current = ''
    },
    sign () {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
  padding: 5px 10px;
}
.btn {
  background-color: #eee;
  border: 1px solid #333;
  padding: 5px 10px;
  cursor: pointer;
}
.zero {
  grid-column: 1/3;
}
.operator {
  background-color: orange;
  color: #ffffff;
}
</style>
