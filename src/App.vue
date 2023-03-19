<script setup>
import {ref} from "vue";

const name = "Vue dinámico";
const counter = ref(0);
const increment = () => {
  counter.value++;
};
const decrement = () => {
  if (counter.value > 0) {
    counter.value--;
  }
};
const reset = () => {
  counter.value = 0;
};
const add = () => {
  arrayFavoritos.value.push(counter.value);
};

const handleClick = (message) => {
  console.log(message);
  // aquí se podría agregar más lógica si se desea
};

const arrayFavoritos = ref([]);

const bloquearBtnAdd = computed (() => {
const numSearch = arrayFavoritos.value.find((num)=>num===counter.value);
console.log(numSearch);
if (numSearch === 0) return true;
return numSearch ? true : false;

});

</script>



<template>
  <h1>Hola {{ name.toUpperCase() }}</h1>
  <button v-on:click.right.prevent="handleClick('Texto Right')">
    Activame right
  </button>
  <button @click="handleClick('Texto Left')">Activame left</button>
  <button @click.middle="handleClick('Texto Middle')">Activame middle</button>

  <h1>--------------------------separador---------------------</h1>
  <h2 :class="counter > 0 ? 'positive' : counter === 0 ? 'neutral' : 'negative'">
    {{ counter }}
  </h2>

  <button @click="increment">Increment</button>
  <button @click="decrement">Decrement</button>
  <button @click="reset">Reset</button>
  <button @click="add" :disabled="bloquearBtnAdd">Add</button>
  <div>Favoritos: {{ arrayFavoritos }}</div>
<ul>
  <li
    v-for ="(num, index) in arrayFavoritos"
    :key="index"
    >
    {{ num }}
  </li>
</ul>



</template>

<style>
  h1 {
    color: red;
  }

  .positive {
    color: aquamarine;
  }

  .neutral {
    color: black;
  }

  .negative {
    color: peru;
  }
</style>
