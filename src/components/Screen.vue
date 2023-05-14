<template>
  <div>{{ screen }}</div>
</template>

<script setup>
const props = defineProps({
  screen: {
    required: true,
  },
});
</script>

<style scoped>
div {
  box-sizing: border-box;
  padding: 35px 30px 25px;
  width: 100%;
  height: 120px;
  border-style: none;
  background-color: transparent;
  color: white;
  text-align: right;
  font-size: 84px;
  font-family: "Courier New", Courier, monospace;
}
</style>
