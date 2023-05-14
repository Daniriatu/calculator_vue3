<template>
  <div class="calculator">
    <Screen :screen="screen" />
    <Keyboard @btnClick="btnClick" />
  </div>
</template>

<script setup>
import Screen from "./Screen.vue";
import Keyboard from "./Keyboard.vue";
import { ref, onMounted } from "vue";

const clearButton = ref("AC");
const screen = ref("0");
const left = ref(0);
const is_new_input = ref(true);
const operateKey = ref("");

const btnClick = (btn) => {
  if ((btn >= "0" && btn <= "9") || btn === ".") {
    appendText(btn);
  } else if (btn === "+" || btn === "-" || btn === "×" || btn === "÷") {
    btnOperator(btn);
  } else if (btn === "=") {
    calculate();
  } else if (btn === "C" || btn === "AC") {
    btnClear();
  } else if (btn === "+/-") {
    btnChangeSymbol();
  } else if (btn === "%") {
    btnPercentage();
  }
};

//AC button
const btnClear = () => {
  if (clearButton.value === "AC") {
    reset();
  }
  clear();
};

//+/- button
const btnChangeSymbol = () => {
  if (screen.value !== "ERROR") {
    screen.value = parseFloat(screen.value) * -1;
  }
};

//% button
const btnPercentage = () => {
  if (screen.value !== "ERROR") {
    screen.value = parseFloat(screen.value) * 0.01;
  }
};

//Show text on the screen
const appendText = (number) => {
  //Decide if a new calculate process started
  if (is_new_input.value) {
    clear();
    is_new_input.value = false;
  }
  //Clean the 0 before the input whole number
  if (screen.value === "0" && number !== ".") {
    screen.value = "";
  }
  //Set all clear to clear
  if (number != "0") {
    clearButton.value = "C";
  }
  //make sure there's only one "."
  if (number === "." && screen.value.indexOf(".") > 0) {
    return;
  }
  //Maximun amount of input number is 7
  if (screen.value.length < 7) {
    screen.value += number;
  }
};

//Clear wrong input number
const clear = () => {
  screen.value = "0";
  clearButton.value = "AC";
};

//Reset all the data
const reset = () => {
  left.value = 0;
  operateKey.value = "";
  is_new_input.value = true;
};

//Get operators
const btnOperator = (keyValue) => {
  if (screen.value !== "ERROR") {
    calculate();
    left.value = parseFloat(screen.value);
    console.log(left.value);
    operateKey.value = keyValue;
    is_new_input.value = true;
  }
};

function calculate() {
  // Store the temp value
  const right = parseFloat(screen.value);
  console.log(right);

  try {
    // Calculate only if there is an operator and no new input number
    if (operateKey.value !== "" && is_new_input.value !== true) {
      let answer;
      switch (operateKey.value) {
        case "+":
          answer = left.value + right;
          break;
        case "-":
          answer = left.value - right;
          break;
        case "×":
          answer = left.value * right;
          break;
        case "÷":
          if (right === 0) {
            answer = "ERROR";
          } else {
            answer = left.value / right;
          }
          break;
        default:
          answer = "ERROR";
      }
      // Decide output result
      if (answer !== "ERROR") {
        screen.value = answer;
      } else {
        screen.value = "ERROR";
      }
      clearButton.value = "AC";
    }
    //Catch unexpected error and output to console.
  } catch (e) {
    screen.value = "ERROR";
    clearButton.value = "AC";
    console.log(e);
  } finally {
    reset();
  }
}

onMounted(() => {
  clear();
});
</script>

<style scoped>
.calculator {
  display: flex;
  box-sizing: border-box;
  margin: 100px auto;
  padding: 1px;
  width: 50%;
  max-width: 430px;
  min-width: 330px;
  border-radius: 10px;
  background-color: #999;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
