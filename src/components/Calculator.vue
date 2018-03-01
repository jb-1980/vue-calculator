<template>
  <div class="calculator">
    <div class="screen">{{expression}}</div>
    <calculator-button
      v-for="b in buttons"
      :key="b.value"
      :value="b.value"
      :class-name="b.className"
      :click-handler="clickButton">
    </calculator-button>
  </div>
</template>

<script>
import CalculatorButton from "./CalculatorButton";

export default {
  name: "Calculator",
  components: { CalculatorButton },
  data: function() {
    return {
      expression: "",
      buttons: [
        { value: "AC", className: "ac" },
        { value: "del", className: "ce" },
        { value: "%", className: "percent" },
        { value: "÷", className: "divide" },
        { value: "7", className: "seven" },
        { value: "8", className: "eight" },
        { value: "9", className: "nine" },
        { value: "×", className: "times" },
        { value: "4", className: "four" },
        { value: "5", className: "five" },
        { value: "6", className: "six" },
        { value: "−", className: "minus" },
        { value: "1", className: "one" },
        { value: "2", className: "two" },
        { value: "3", className: "three" },
        { value: "+", className: "add" },
        { value: "0", className: "zero" },
        { value: ".", className: "period" },
        { value: "=", className: "equal" }
      ]
    };
  },
  methods: {
    clickButton: function(event) {
      const v = event.target.innerText;

      // reset expression if it currently displays syntax error
      if (this.expression === "Syntax Error") {
        this.expression = "";
      }
      switch (v) {
        case "AC":
          // reset the expression
          this.expression = "";
          break;
        case "del":
          // clear the last entry
          this.expression = this.expression.slice(0, -1);
          break;

        case "%":
          // present the result as a percent
          if (isNaN(this.expression)) {
            this.expression = "Syntax Error";
          } else {
            this.expression = this.expression * 100 + "%";
          }
          break;

        case "÷":
          this.expression += "/";
          break;

        case "×":
          this.expression += "*";
          break;

        case "−":
          this.expression += "-";
          break;

        case "=":
          try {
            this.expression = String(eval(this.expression));
          } catch (e) {
            if (e instanceof SyntaxError) {
              this.expression = "Syntax Error";
            } else {
              throw e;
            }
          }
          break;

        default:
          this.expression += v;
      }
    }
  }
};
</script>

<style>
.calculator {
  width: 200px;
  height: 400px;
  background: salmon;
  border: thick solid brown;
  border-radius: 20px;
  margin: auto;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: repeat(6, 1fr);
  grid-template-areas:
    "screen screen screen screen"
    "AC CE percent divide"
    "seven eight nine times"
    "four five six minus"
    "one two three add"
    "zero period equal add";
  grid-gap: 5px;
  padding: 5px;
}
.screen {
  grid-area: screen;
  background: gray;
  border-radius: 20px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  font-size: 30px;
  line-height: 30px;
  font-family: "Digital-7 Mono";
}

.button {
  background: #e05e4f;
  border-radius: 20px;
  border: 2px solid #e05e4f;
  justify-content: center;
  align-items: center;
  display: flex;
  font-size: 20px;
  cursor: pointer;
}

.add {
  grid-area: add;
}
</style>
