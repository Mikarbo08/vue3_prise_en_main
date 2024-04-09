<template>
  <section>
    <label>Kelvin</label>
    <input type="number" :value="round(kelvin)" @input="kelvin = parse($event.target.value)">
    <label>Celsius</label>
    <input type="number" :value="round(celsius)" @input="celsius = parse($event.target.value)">
    <label>Fahrenheit</label>
    <input type="number" :value="round(fahrenheit)" @input="fahrenheit = parse($event.target.value)">
  </section>
</template>

<script setup>
import { ref, computed } from 'vue';

const kelvin = ref('');
const round = (val) => (val === '') ? '' : parseFloat(val.toFixed(2)).toString();
const parse = (val) => (val === '') ? '' : parseFloat(val);

const celsius = computed({
  get: () => (kelvin.value === '') ? '' : kelvin.value - 273.15,
  set: (c) => { kelvin.value = (c === '') ? '' : c + 273.15; }
});

const fahrenheit = computed({
  get: () => (kelvin.value === '') ? '' : kelvin.value * 1.8 - 459.67,
  set: (f) => { kelvin.value = (f === '') ? '' : (f + 459.67) / 1.8; }
});
</script>

<style scoped>
section {
  margin: 2rem;
  display: grid;
  gap: 1rem;
}
input, label {
  font-size: 1.5rem;
}
input {
  height: 2rem;
  width: 100%;
  max-width: 18rem;
}
</style>