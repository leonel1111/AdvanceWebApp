<script setup>
import { ref } from 'vue';

const inputWeight = ref('');
const initialUnit = ref('');
const selectedUnit = ref('');
const convertedWeight = ref(null);

const convertWeight = () => {
  const weight = parseFloat(inputWeight.value);

  if (isNaN(weight)|| initialUnit.value === '' || selectedUnit.value === '') {
    // Handle invalid input (non-numeric)
    window.alert('Please fill out all the fields.');
    convertedWeight.value = null;
  } else {
    const initialUnitToKg = {
      kg: 1,
      g: 0.001,
      mg: 0.000001,
      lb: 0.453592,
      t: 1000,
    };

    const kgToSelectedUnit = {
      kg: 1,
      g: 1000,
      mg: 1000000,
      lb: 2.20462,
      t: 0.001,
    };

    const weightInKg = weight * initialUnitToKg[initialUnit.value];
    convertedWeight.value = weightInKg * kgToSelectedUnit[selectedUnit.value];
  }
};
</script>


<template>
  <div class="container mt-5">
    <h1 class="text-center">Weight Converter</h1>
    

  <div class="row">
    <div class="col-md-6">
      <div class="form-group">
        <label for="iWeight">Enter Weight:</label>
        <input type="text" class="form-control" id="iWeight" v-model="inputWeight">
      </div>
    </div>
    <div class="col-md-6">
      <div class="form-group">
        <label for="initialUnit">From:</label>
        <select class="form-control" name="initialUnit" id="initialUnit" v-model="initialUnit">
          <option value="" disabled>Select weight unit</option>
          <option value="kg">Kilograms</option>
          <option value="g">Grams</option>
          <option value="mg">Milligrams</option>
          <option value="lb">Pounds</option>
          <option value="t">Ton</option>
        </select>
      </div>
    </div>
</div>
    <div class="form-group">
      <label for="convert">Convert to:</label>
      <select class="form-control" name="convert" id="convert" v-model="selectedUnit">
  <option value="" disabled>Select weight unit</option>
  <option value="kg">Kilograms</option>
  <option value="g">Grams</option>
  <option value="mg">Milligrams</option>
  <option value="lb">Pounds</option>
  <option value="t">Ton</option>
</select>

    </div>
    <button class="btn btn-primary mx-auto d-block w-50 mt-3" @click="convertWeight">Convert</button>
    <h2 class="mt-3" v-if="convertedWeight !== null">Result: {{ convertedWeight.toFixed(2) }} {{ selectedUnit }}</h2>
  </div>





</template>

<style>
.container {
    background-color: white;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
    padding: 20px;
    max-width: 600px;
    margin: 0 auto;
    border-radius: 18px;
    margin-top: 50px;
}
</style>
