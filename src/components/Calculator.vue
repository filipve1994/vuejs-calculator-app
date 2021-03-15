<template>
  <div id="calculator" class="calculator">
    <div class="display">{{ display }}</div>
    <h1 class="brand">{{ appTitle }}</h1>
    <div class="keyboard">
      <div class="panel-a">
        <div class="top-buttons">
          <button class="btn primary" @click="clear"><span>C </span></button>
          <button class="btn" @click="setNumber('.')"><span>.</span></button>
        </div>
        <div class="numbers">
          <button class="btn" @click="setNumber('9')"><span>9</span></button>
          <button class="btn" @click="setNumber('8')"><span>8</span></button>
          <button class="btn" @click="setNumber('7')"><span>7</span></button>
          <button class="btn" @click="setNumber('6')"><span>6</span></button>
          <button class="btn" @click="setNumber('5')"><span>5</span></button>
          <button class="btn" @click="setNumber('4')"><span>4</span></button>
          <button class="btn" @click="setNumber('3')"><span>3</span></button>
          <button class="btn" @click="setNumber('2')"><span>2</span></button>
          <button class="btn" @click="setNumber('1')"><span>1</span></button>
          <button class="btn" @click="setNumber('0')"><span>0</span></button>
        </div>
      </div>
      <div class="panel-b">
        <button class="btn" @click="operator = '+'"><span>+</span></button>
        <button class="btn" @click="operator = '-'"><span>-</span></button>
        <button class="btn" @click="operator = '*'"><span>*</span></button>
        <button class="btn" @click="operator = '/'"><span>/</span></button>
        <button class="btn primary" @click="calculate"><span>=</span></button>
      </div>
    </div>
  </div>
</template>

<!--https://codepen.io/Paolo-Duzioni/pen/Jyxzom -->
<script>
export default {
  name: "Calculator",
  data() {
    return {
      appTitle: "Vue Calculator",
      a: "",
      b: "",
      tot: 0,
      display: 0,
      operator: null
    };
  },
  methods: {
    setNumber(num) {
      if (this.operator === null) {
        this.a += num;
        this.display = this.a;
      } else {
        this.b += num;
        this.display = this.b;
      }
    },

    calculate() {
      switch (this.operator) {
        case "+":
          this.tot = parseFloat(this.a) + parseFloat(this.b);
          break;
        case "-":
          this.tot = parseFloat(this.a) - parseFloat(this.b);
          break;
        case "*":
          this.tot = parseFloat(this.a) * parseFloat(this.b);
          break;
        case "/":
          this.tot = parseFloat(this.a) / parseFloat(this.b);
          break;
      }
      this.display = this.tot;
      this.a = "" + this.tot + "";
      this.b = "";
      this.operator = null;
    },

    clear() {
      this.a = "";
      this.b = "";
      this.tot = 0;
      this.display = 0;
      this.operator = null;
    }
  }
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
//FONTS
@import url("https://fonts.googleapis.com/css?family=Bungee+Hairline");
$font-primary: "Bungee Hairline", cursive;

// COLORS
$white: #fff;
$black: #000;
$calc-col: #eee;
$btn-col: #333;
$primary-btn: dodgerblue;

// GENERAL
*,
*::before,
*::after {
  box-sizing: border-box;
}
body,
#calculator {
  background: $black;
  font-family: $font-primary;
  font-size: 16px;
}

// CALCULATOR STYLES
.calculator {
  width: 30rem;
  max-width: 100%;
  margin: 3rem auto;
  padding: 0.3rem;
  .display {
    height: 4rem;
    line-height: 4rem;
    margin: 0 0.3rem;
    padding: 0 0;
    text-align: right;
    font-size: 1.5em;
    color: $white;
    border-bottom: 1px solid rgba($white, 0.15);
  }
  .brand {
    margin: 0.6rem 0 0.3rem;
    padding: 0 0.3rem;
    text-align: right;
    font-size: 0.65em;
    color: rgba($white, 0.85);
  }
  .keyboard {
    display: flex;
    flex-wrap: wrap;
    .btn {
      margin: 0;
      padding: 0;
      height: 4.6rem;
      line-height: 4rem;
      text-align: center;
      font-family: inherit;
      font-size: 1.25em;
      border: none;
      background: transparent;
      outline: none;
      &:hover {
        span {
          background: lighten($btn-col, 10%);
        }
      }
      span {
        display: block;
        margin: 0.3rem;
        color: $white;
        background: $btn-col;
        border-radius: 3px;
        transition: background-color 0.4s;
      }
      &.primary {
        &:hover {
          span {
            background: lighten($primary-btn, 15%);
          }
        }
        span {
          background: $primary-btn;
        }
      }
    }
    .panel-a {
      width: 75%;
      .top-buttons {
        .btn {
          width: 33.3%;
          &:last-of-type {
            float: right;
          }
          span {
            font-weight: bold;
          }
        }
      }
      .numbers {
        display: flex;
        flex-wrap: wrap;
        flex-direction: row-reverse;
        align-items: flex-end;
        align-content: flex-end;
        .btn {
          width: 33.3%;
          &:nth-child(10) {
            width: 100%;
          }
        }
      }
    }
    .panel-b {
      display: flex;
      flex-direction: column;
      width: 25%;
      .btn {
        width: 100%;
        span {
          font-weight: bold;
        }
      }
    }
  }
}
</style>
