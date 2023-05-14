<template>
  <Button class="btn-secondary" text="AC" @btnClick="btnClick"></Button>
  <Button class="btn-secondary" text="+/-" @btnClick="btnClick"></Button>
  <Button class="btn-secondary" text="%" @btnClick="btnClick"></Button>

  <Button class="btn-operator" text="÷" @btnClick="btnClick"></Button>

  <Button class="btn-number" text="7" @btnClick="btnClick"></Button>
  <Button class="btn-number" text="8" @btnClick="btnClick"></Button>
  <Button class="btn-number" text="9" @btnClick="btnClick"></Button>

  <Button class="btn-operator" text="×" @btnClick="btnClick"></Button>

  <Button class="btn-number" text="4" @btnClick="btnClick"></Button>
  <Button class="btn-number" text="5" @btnClick="btnClick"></Button>
  <Button class="btn-number" text="6" @btnClick="btnClick"></Button>

  <Button class="btn-operator" text="-" @btnClick="btnClick"></Button>

  <Button class="btn-number" text="1" @btnClick="btnClick"></Button>
  <Button class="btn-number" text="2" @btnClick="btnClick"></Button>
  <Button class="btn-number" text="3" @btnClick="btnClick"></Button>

  <Button class="btn-operator" text="+" @btnClick="btnClick"></Button>

  <Button
    class="btn-large btn-number btn-bottom-left"
    text="0"
    @btnClick="btnClick"
  ></Button>
  <Button class="btn-number" text="." @btnClick="btnClick"></Button>

  <Button
    class="btn-equal btn-bottom-right"
    text="="
    @btnClick="btnClick"
  ></Button>
</template>

<script setup>
import Button from "./Button.vue";

const emit = defineEmits(["btnClick"]);

const btnClick = (btn) => {
  emit("btnClick", btn);
};
</script>

<style scoped>
.keypad {
  display: flex;
  box-sizing: border-box;
  max-width: 430px;
  min-width: 330px;
  border-radius: 10px;
  background-color: #999;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  flex-direction: row;
  flex-wrap: wrap;
  margin: 0;
  padding: 0;
  width: 100%;
}

.btn-operator,
.btn-equal {
  background-color: #f69232;
  color: #fff;
  font-size: 48px;
  font-family: "Courier New", Courier, monospace;
}

.btn-operator:active,
.btn-equal:active {
  background-color: #ba7737;
  color: #000;
}

.btn-secondary {
  background-color: #d6d6d6;
  font-size: 32px;
}

.btn-secondary:active {
  background-color: #a9a9a9;
}

.btn-number {
  background-color: #e0e0e0;
  font-size: 36px;
}

.btn-number:active {
  background-color: #b2b2b2;
}

.btn-large {
  padding-right: calc(24% + 8px);
  flex: 1 1 49%;
}

.btn-bottom-left {
  border-radius: 0 0 0 9px;
}

.btn-bottom-right {
  border-radius: 0 0 9px 0;
}
</style>
