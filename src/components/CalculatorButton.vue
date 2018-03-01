<template>
  <div class="button" :class="className" v-on:click="clickHandler">{{value}}</div>
</template>

<script>
export default {
  name: "CalculatorButton",
  props: ["clickHandler", "value", "className"]
};
</script>

<style>
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
</style>
