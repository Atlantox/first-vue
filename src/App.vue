<script setup>
import {ref} from 'vue'

const maxAvailablePoints = 35;
const availablePoints = ref(maxAvailablePoints);

const tableHead = [
  'Statistic',
  'Value',
  'Add',
  'Remove',
  'Dice modifier'
];

const statisticsList = ref([
  {
    'name': 'Strength',
    'value': 5
  },
  {
    'name': 'Destrerity',
    'value': 5
  },
  {
    'name': 'Intelligence',
    'value': 5
  },
  {
    'name': 'Perception',
    'value': 5
  },
  {
    'name': 'Constitution',
    'value': 5
  },
  {
    'name': 'Knowledge',
    'value': 5
  },
  {
    'name': 'Charisma',
    'value': 5
  }
]);

const modifyStatistic = (statisticIndex, value) => {
  const statisticValue = statisticsList.value[statisticIndex].value;
  const result = statisticValue + value;
  const avaliablePointsResult = availablePoints.value - value;
  if(avaliablePointsResult < 0){
    alert('Not enought points');
  }
  else{
    let tentativeValue = null;
    if (result < 5){
      if (statisticValue === 5)
        alert('A statistic cannot be lower than 5');
      else
        tentativeValue = 5;
    }
    else if (result > 15){
      if (statisticValue === 15)
        alert('A statistic cannot be greater than 15');
      else
        tentativeValue = 15;
    } 
    else {
      availablePoints.value -= value;
      statisticsList.value[statisticIndex].value = result;  
    }

    if(tentativeValue !== null){
      const diff = tentativeValue - statisticValue;
      availablePoints.value -= diff
      statisticsList.value[statisticIndex].value = tentativeValue;
    }
  }
}

const getDiceModifier = (statistic) => {
  const normalStat = 10;
  const diff = statistic.value - normalStat;
  if(diff < 0) return Math.ceil(diff / 2);
  else return '+' + Math.floor(diff / 2);
};

const getDiceModifierColor = (value) => {
  if (value === 0) return 'text-white';
  else if (value > 0) return 'text-green';
  else return 'text-red';
};
</script>

<template>
  <div class="row col-8">
    <div class="row justify-content-center">
      <h1 class="text-center mb-5">Roleplay statistic manager</h1>
      <h4 class="col-8">
        Rules
      </h4>
      <ul class="col-8">
        <li>A statistic cannot be greater than 15 or lower than 5</li>
        <li>You will have 35 poins to distribute as you like</li>
        <li>Right click a button to do +5 or -5</li>
      </ul>
      <h3 class="text-center w-100">Available points: {{ availablePoints }}</h3>
    </div>
    <div class="row justify-content-center">
      <div class="col-12 row justify-content-center">
        <table class="col-10">
          <thead>
            <tr>
              <th 
              v-for="column in tableHead"
              :key="column"
              class="fw-bold px-3 text-center border border-1"
              >
              {{ column }}
              </th>
            </tr>
          </thead>

          <tbody>
            <tr
            v-for="(statistic, index) in statisticsList"
            :key="index"
            class="text-center border-1"
            >
              <td class="px-1">{{ statistic.name }}</td>
              <td class="h5">{{ statistic.value }}</td>
              <td class="p-1">
                <button
                v-on:click.left="modifyStatistic(index, 1)"
                v-on:click.right.prevent="modifyStatistic(index, 5)"
                class="btn btn-success h1 fw-bold text-center align-middle"> + </button>
              </td>
              <td>
                <button 
                v-on:click.left="modifyStatistic(index, -1)"
                v-on:click.right.prevent="modifyStatistic(index, -5)"
                class="btn btn-danger h1 fw-bold text-center align-middle"> - </button>
              </td>
              <td 
                class="fw-bold h5 text-shadow"
                :class="getDiceModifierColor(getDiceModifier(statistic))">
                {{ getDiceModifier(statistic) }}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style>
body{
  background-color:rgb(83, 83, 83) !important;
  color:rgb(231, 231, 231) !important;
}

td{
  border: #dee2e6 1px solid !important;
}

.text-green{
  color:rgb(0, 182, 0) !important;
}

.text-red{
  color:rgb(248, 51, 51) !important;
}

.text-shadow{
  text-shadow: black 0px 0px 3px;
}
</style> 