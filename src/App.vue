<script setup>
  import { ref, computed } from 'vue'; //referencia reactiva

  const name = "Vue3"

  //Methods:
  const counter = ref(0); //devuelve objeto con propiedad ".value"
  const arrayFavoritos = ref([])

  const increment = () => counter.value ++; //acceder a valor real con .value
  const decrease = () => counter.value -- //counter substract
  const valueReset = () => (counter.value = 0) //counter reset

  const add = () => {
    arrayFavoritos.value.push(counter.value)
  }

  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find((num) => num === counter.value) //busca si el numero que queremos agregar al array ya fue agregado
    return numSearch || numSearch === 0 //numSearch devuelve true o false(dependiendo si el numero existe o no y numSearch === 0 si es igual a zero nos devuelve un true)
  })

  const classCounter = computed(() => {
    if(counter.value === 0) {
      return 'zero_num'
    }
    if(counter.value > 0) {
      return 'positive_num'
    }
    if(counter.value < 0) {
      return 'negative_num'
    }
  }) 
</script>

<template>
<div class="container text-center">
  <div class="row">
    <div class="col-9">
      <h1>Mi primera App con nombre: {{ name.toUpperCase() }}</h1>
      <h2 :class="classCounter">{{ counter }}</h2> 
      <div class="btn-group" role="group" aria-label="Basic example">
        <button @click="decrease" class="btn btn-danger">Restar ➖</button> 
        <button @click="valueReset" class="btn btn-secondary">Reset 0️⃣</button>
        <button @click="increment" class="btn btn-success">Incrementar ➕</button>
        <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-warning">Add Favorite💖</button>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col-9">
      <ul class="list-group mt-4">
        <li v-for="(number, index) in arrayFavoritos" :key="index" class="list-group-item">{{ number }}</li>
      </ul>
    </div>
  </div>
</div>
</template>

<style>
  h1 {
    color:aqua;
  }

  .positive_num {
    color: green;
  }

  .negative_num {
    color: red;
  }

  .zero {
    color: azure;
  }

  
</style>
