<template>
  <button @click="btnClick">{{ text }}</button>
</template>

<script setup>
//Recive button text data from Keyboard Component
const props = defineProps({
  text: String,
});

// Use defineEmit to pass clicked button text to Keyboard Component
const emit = defineEmits(["btnClick"]);

const btnClick = () => {
  emit("btnClick", props.text);
};
</script>

<style scoped>
button {
  margin: 1px;
  height: 80px;
  border-style: none;
  text-align: center;
  font-family: "helvetica_neue", Helvetica, Arial, sans-serif;
  cursor: pointer;
  flex: 1 1 24%;
}

button:focus {
  outline: none;
}
</style>
