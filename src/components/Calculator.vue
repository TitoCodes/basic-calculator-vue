<template>
  <div class="calculator-container">
    <div>TitoCodes Calculator</div>
    <span>
      Made using
      <span>Vue.js</span>
    </span>
    <br />

    <div>
      <input v-on:keyPress="addToParam($event)" readonly type="text" v-model="result" />
    </div>
    <div>
      <button v-on:click="addToParam(7)">7</button>
      <button v-on:click="addToParam(8)">8</button>
      <button v-on:click="addToParam(9)">9</button>
      <button v-on:click="selectOperator('multiply')">*</button>
    </div>

    <div>
      <button v-on:click="addToParam(4)">4</button>
      <button v-on:click="addToParam(5)">5</button>
      <button v-on:click="addToParam(6)">6</button>
      <button v-on:click="selectOperator('subtract')">-</button>
    </div>

    <div>
      <button v-on:click="addToParam(1)">1</button>
      <button v-on:click="addToParam(2)">2</button>
      <button v-on:click="addToParam(3)">3</button>
      <button v-on:click="selectOperator('add')">+</button>
    </div>

    <div>
      <button v-on:click="addToParam(0)">0</button>
      <button v-on:click="clearResult()">AC</button>
      <button v-on:click="executeOperation()">=</button>
      <button v-on:click="selectOperator('divide')">/</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data: function () {
    return {
      result: 0,
      param: [],
      resultHolder: 0,
      currentOperator: "",
    };
  },
  methods: {
    addToParam: function (number) {
      if (this.param.length > 13) {
        return;
      }

      const notANumber = /\D/;

      if (typeof number !== "number") {
        if (!number.key.match(notANumber)) {
          number = number.key;
        } else {
          return;
        }
      }
      this.param.push(number);
      this.result = this.param.join("");
    },
    clearResult: function () {
      this.resultHolder = 0;
      this.currentOperator = "";
      this.result = 0;
      this.param = [];
    },
    selectOperator: function (selectedOperator) {
      this.currentOperator = selectedOperator;
      this.resultHolder = this.result;
      this.param = [];
    },
    executeOperation: function () {
      this.resultHolder = Number(this.resultHolder);
      this.result = Number(this.result);

      if (this.currentOperator === "add") {
        this.result = this.resultHolder + this.result;
      } else if (this.currentOperator === "subtract") {
        this.result = this.resultHolder - this.result;
      } else if (this.currentOperator === "divide") {
        this.result = this.resultHolder / this.result;
      } else if (this.currentOperator === "multiply") {
        this.result = this.resultHolder * this.result;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  text-align: right;
}
.calculator-container > div {
  font-size: 24px;
}
.calculator-container > span {
  font-size: 12px;
  font-style: italic;
}
.calculator-container > span > span {
  color:green;
}
</style>
