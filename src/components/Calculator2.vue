<template>
  <section
    id=""
    class="hero is-light is-bold is-fullheight"
    @keyup="console.log"
  >
    <div class="hero-body">
      <div class="container">
        <div class="calc">
          <div class="overview" v-if="previousNumber && operator">
            {{ previousNumber }} {{ operator }} {{ number }}
          </div>

          <input
            type="number"
            class="calc input"
            name="number"
            v-model="number"
            v-if="!placeholder"
          />
          <input
            type="number"
            class="calc input"
            name="number"
            v-model="placeholder"
            v-if="placeholder"
          />

          <div class="calc-buttons">
            <button class="calc-button is-clear" @click="clear">C</button>
            <button
              class="calc-button is-operator"
              @click="selectOperator('/')"
            >
              &divide;
            </button>

            <button class="calc-button" @click="appendNumber('7')">7</button>
            <button class="calc-button" @click="appendNumber('8')">8</button>
            <button class="calc-button" @click="appendNumber('9')">9</button>
            <button
              class="calc-button is-operator"
              @click="selectOperator('*')"
            >
              &times;
            </button>

            <button class="calc-button" @click="appendNumber('4')">4</button>
            <button class="calc-button" @click="appendNumber('5')">5</button>
            <button class="calc-button" @click="appendNumber('6')">6</button>
            <button
              class="calc-button is-operator"
              @click="selectOperator('-')"
            >
              &minus;
            </button>

            <button class="calc-button" @click="appendNumber('1')">1</button>
            <button class="calc-button" @click="appendNumber('2')">2</button>
            <button class="calc-button" @click="appendNumber('3')">3</button>
            <button
              class="calc-button is-operator"
              @click="selectOperator('+')"
            >
              &plus;
            </button>

            <button class="calc-button is-0" @click="appendNumber('0')">
              0
            </button>
            <button
              class="calc-button is-operator is-equals"
              @click="calculate"
            >
              =
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<!--https://codepen.io/chris__sev/pen/RQGeLV -->
<script>
export default {
  name: "Calculator2",
  data() {
    return {
      number: 0,
      previousNumber: null,
      placeholder: null,
      operator: null
    };
  },
  methods: {
    appendNumber: function(number) {
      if (this.placeholder) {
        this.placeholder = null;
        this.number = number;
        return;
      } else if (this.number === 0) {
        this.number = number;
        return;
      }

      this.number = this.number + number;
    },
    selectOperator: function(operator) {
      if (this.number === 0) return;

      this.previousNumber = this.number;
      this.placeholder = this.number;
      this.number = null;
      this.operator = operator;
    },
    clear: function() {
      this.number = 0;
      this.previousNumber = null;
      this.placeholder = null;
      this.operator = null;
    },
    calculate: function() {
      switch (this.operator) {
        case "+":
          this.number = +this.previousNumber + +this.number;
          break;
        case "-":
          this.number = this.previousNumber - this.number;
          break;
        case "*":
          this.number = this.previousNumber * this.number;
          break;
        case "/":
          this.number = this.previousNumber / this.number;
          break;
      }

      this.operator = null;
      this.previousNumber = null;
      this.placeholder = null;
    }
  }
};
</script>

<style scoped lang="scss">
.calc {
  max-width: 400px;
  margin: 0 auto;
  border: 2px solid #111;
  border-radius: 5px;
}

.overview {
  text-align: right;
  padding-top: 20px;
  padding-right: 40px;
}

.calc input {
  font-family: "Space Mono", monospace;
  background: none;
  border: none;
  border-bottom: 2px solid #111;
  box-shadow: none;
  outline: none;
  color: #333;
  text-align: right;
  font-size: 40px;
  border-radius: 0;
}

.calc input:hover,
.calc input:focus {
  border-color: #000;
  outline: none;
  box-shadow: none;
}

.calc-buttons {
  padding: 20px;
  display: grid;
  grid-template-rows: repeat(5, 1fr);
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 15px;
  text-align: center;
}

.calc-button {
  font-family: "Space Mono", monospace;
  background: rgba(0, 0, 0, 0.5);
  border: 1px solid #111;
  padding: 20px;
  border-radius: 5px;
  color: #eee;
  font-size: 22px;
  line-height: 1;
  cursor: pointer;
  transition: 0.2s ease all;
}

.calc-button:hover,
.calc-button:focus {
  background: rgba(0, 0, 0, 0.75);
  outline: none;
}

.is-clear {
  background: #3572db;
}

.is-equals {
  background: #28d060;
}

.is-0,
.is-clear {
  grid-column: span 3;
}
</style>
