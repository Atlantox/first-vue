<script setup>
  import {ref, computed} from 'vue'

  const name = 'Pedrito Oropeza';
  const wata_style = 'color:blue;';
  const wata_id = 'watagatapitusberry';
  const good_people = ['Escanor', 'Maau', 'RanguGamer', 'The Rock'];
  const my_fruits = ['banana', 'mango', 'manzana', 'guayaba', 'limón'];
  const my_colors = ['red', 'peru', 'violet'];
  const super_fruits = [
    {
      name:"Manzana",
      price: '$1.00',
      description: 'Una manzana',
      stock: 8
    },
    {
      name:"Pera",
      price: '$2.00',
      description: 'Una pera',
      stock: 3
    },
    {
      name:"Cambur",
      price: '$3.00',
      description: 'Un cambur',
      stock: 14
    }
  ];

  const my_fruit_object = {
    name:"Guanabana",
    price: '$8.0',
    description: 'Fascinante'
  };
  const active = true;
  const possible = null;

  const handleClick = (message) => {
      console.log('mostrando: ' + message);
    };

  const counter = ref(0);
  const due = ref(true);

  const toggleDue = () => {
    due.value = !due.value;
  }

  const incrementer = () => {
    counter.value++;
    toggleDue();
  }

  const decrementer = () => {
    counter.value--;
    toggleDue();
  };

  const classToggler = computed(() => {
    if(counter.value === 0) return 'zero';
    else if(counter.value > 0) return 'positive';
    else return 'negative';
  });
</script>


<template>
  <h1>Good night {{ name.toUpperCase() }}</h1>
  <h2 :style="wata_style" :id="wata_id">Watagatapitusberry WHAT</h2>
  <h3 :style="`color:${my_colors[2]}`" >{{ good_people }}</h3>
  <h3>{{ active ? 'Activo papi' : 'Inactivo, pa' }}</h3>
  <h1 v-if="possible">Posible</h1>
  <h1 v-else-if="possible === false">Imposible</h1>
  <h1 v-else>No estoy seguro</h1>
  <h1 v-show="active">Este es el active v-show</h1>
  <h1>Frutitas</h1>
  <ul>
    <li 
      v-for="(fruit, index) in my_fruits"
      :key="index"
    >
      {{ index + 1 }}: {{ fruit }}
    </li>
  </ul>
  <br>
  <ul>
    <li
      v-for="(fruit) in super_fruits"
      :key="fruit.name"
    >
      <h4>{{ fruit.name }}</h4>
      <h6>{{ fruit.price }}</h6>
      <p>{{ fruit.description }}</p>

    </li>
  </ul>
  <br>
  <ul>  
    <li
      v-for="(value, key, index) in my_fruit_object"
      :key="index"
    >
      {{ index }} -- {{ key }} : {{ value }}
    </li>
  </ul>

  <ul>
    <h1>Conditional for</h1>
    <template
      v-for="fruit in super_fruits"
        :key="fruit.name"
      >
      <li v-if="fruit.stock >= 10">
          {{ fruit.name }}
      </li>
    </template>
  </ul>

  <button v-on:click ="handleClick('click izquierdo')">left click me!</button>
  <button v-on:click.middle ="handleClick('click central')">center click me!</button>
  <button v-on:click.right.prevent ="handleClick('click derecho')">right click me!</button>
  <br>
  <div>
    <h2 :class="classToggler" >{{ counter }} : {{ due }}</h2>
    <section>
      <button v-on:click="incrementer">Incrementar contador</button>
      <button v-on:click="decrementer">Decrementar contador</button>
    </section>

  </div>
</template>

<style>
h1{
  color:#8709b4;
}

.positive {
  color:green
}

.negative{
  color: red;
}

.zero{
  color:#8709b4;
}
</style>