<script setup>
import {ref, computed} from 'vue'

const counter = ref(0);
const savedNumbers = ref([]);

const modifyCounter = (quantity) => {
  counter.value += quantity;
};

const saveNumber = () => {
  if (!savedNumbers.value.includes(counter.value))
    savedNumbers.value.push(counter.value);
  else
    alert('numero repetido');
};

const titleClass = computed(() => {
  if (counter.value === 0) return 'zero';
  else if (counter.value > 0) return 'positive';
  else return 'negative';
});
</script>

<template>
  <h1 class="text-center" :class="titleClass">{{ counter }}</h1>
  <br>
  <div class="text-center">
    <button v-on:click.left="modifyCounter(-1)" v-on:click.right.prevent="modifyCounter(-10)">Disminuir</button>
    <button v-on:click="modifyCounter(-counter)">Resetar</button>
    <button v-on:click.left="modifyCounter(1)" v-on:click.right.prevent="modifyCounter(10)">Aumentar</button>
  </div>
  <br><br>
  <div class="text-center">
    <button @:click="saveNumber" class="w-100">Agregar número a favoritos</button>
  </div>
  <br>
  <div class="w-100 text-center">
    <span
      v-for="number in savedNumbers"
      :key="number"
    >
      &nbsp; {{ number }} &nbsp;
    </span>
  </div>
</template>

<style>
h1{
  font-size: 60px;
}

ul{
  list-style-type: none;
  padding: 0;
  margin: 10px 0 0 0;
  font-size: 20px;
}

.text-center{
  text-align: center;
}

button{
  padding:5px;
  font-size: 20px;
  border-radius: 10px;
  margin:5px;
}

.w-100{
  width:100%;
}

.positive{
  color:green;
}

.negative{
  color:red;
}

.zero{
  color:grey;
}
</style> 