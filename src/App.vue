<template>
  <div id="app">
    <div class="main">
      <div class="display">{{ displayValue }}</div>
      <div class="button-container">
        <div class="button gray" @click="setOperator('ac')">AC</div>
        <div class="button gray" @click="setOperator('+/-')">+/-</div>
        <div class="button gray" @click="setOperator('%')">%</div>
        <div class="button orange" @click="setOperator('/')">/</div>
        <div class="button" @click="setDigit('7')">7</div>
        <div class="button" @click="setDigit('8')">8</div>
        <div class="button" @click="setDigit('9')">9</div>
        <div class="button orange" @click="setOperator('*')">x</div>
        <div class="button" @click="setDigit('4')">4</div>
        <div class="button" @click="setDigit('5')">5</div>
        <div class="button" @click="setDigit('6')">6</div>
        <div class="button orange" @click="setOperator('-')">-</div>
        <div class="button" @click="setDigit('1')">1</div>
        <div class="button" @click="setDigit('2')">2</div>
        <div class="button" @click="setDigit('3')">3</div>
        <div class="button orange" @click="setOperator('+')">+</div>
        <div class="button" id="zero" @click="setDigit('0')">0</div>
        <div class="button" @click="setDigit('.')">.</div>
        <div class="button orange" @click="setOperator('=')">=</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      value: "0",
      temp: 0,
      op: "",
      isPoint: false
    };
  },
  methods: {
    setDigit(val) {
      // if (this.op != "") {
      // } else {
      //   this.value = this.value * 10 + val;
      // }
      if (this.value === "0" && val != ".") {
        this.value = val;
      } else {
        this.value += val;
      }
    },
    setOperator(op) {
      if (op === "ac" || op === "+/-" || op === "%") this.calculator(op);
      else {
        if (this.op != "") this.calculator(this.op);
        else {
          this.temp = parseFloat(this.value);
        }
        this.op = op;
        this.value = "0";
      }
    },
    calculator(op) {
      switch (op) {
        case "ac":
          this.value = "0";
          this.temp = 0;
          break;
        case "+/-":
          if (this.value.includes("-")) {
            this.value = this.value.substring(1);
          } else {
            this.value = "-" + this.value;
          }
          break;
        case "%":
          this.value = this.value / 100;
          break;
        case "/":
          this.temp /= parseFloat(this.value);
          break;
        case "*":
          this.temp *= parseFloat(this.value);
          break;
        case "-":
          this.temp -= parseFloat(this.value);
          break;
        case "+":
          this.temp += parseFloat(this.value);
          break;
        case "=":
          break;
      }
    }
  },
  computed: {
    displayValue() {
      return this.op != "" && this.value === "0" ? this.temp : this.value;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 500px;
  width: 280px;
}
.main {
  padding: 1%;
  height: 100%;
  width: 100%;
  background: #000;
}
.display {
  width: 100%;
  height: 30%;
  color: #fff;
  text-align: right;
  font-size: 4rem;
  line-height: 3em;
}
.button-container {
  width: 100%;
  height: 70%;
  display: grid;
  grid-template-columns: auto auto auto auto;
  justify-items: center;
  // padding-bottom: 5px;
  .button {
    line-height: 60px;
    background: #343434;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
    font-weight: 500;
    font-size: 1.5em;
    color: #fff;
    &.gray {
      background: #a6a6a6;
      color: #000;
    }
    &.orange {
      background: #f79706;
    }
  }
  #zero {
    grid-column-start: 1;
    grid-column-end: 3;
    width: 120px;
    border-radius: 30px;
  }
}
</style>
