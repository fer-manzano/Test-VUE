<script setup>

import { ref, computed } from "vue";

// counter ahora es una variable reactiva
const counter = ref(0);

const arrayCounter = ref([]);

const increment = () => {
    // mutamos el valor a través de .value
    counter.value++;
};

const decrement = () => {
    counter.value--;
};

const reset = () => {
    counter.value = 0;
};

const add = () => {
    arrayCounter.value.push(counter.value);
};

const blockNumber = computed(() => {
  //esto retorna booleano es decir, true o false
    const number = arrayCounter.value.find((num) => num === counter.value);

    if(number === 0) return true;
    return number ? true : false;

    //esta es otra opción tiene el mismo resultado que el de arriba
    //return number || number === 0;
});


const classCounter = computed(() => {
    if (counter.value === 0) {
        return "zero";
    }
    return counter.value > 0 ? "positive" : "negative";
});

const name = 'Vue dinámico';
const styleColor = 'color: blue';
const arrayColores = ["blue","red","peru"];
const activo =false;

const arrayFrutas_0 = ["🍎", "🍌", "🍉", "🍓", "🍒"];

const arrayFrutas = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
        },
    ];

    const Objetofruta = {
      name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            id: 1,
    };

    const arrayFrutas2 = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        stock: 0,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        stock: 10,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        stock: 20,
    },
];

// método handleClick

//Sin Parametro
//const handleClick = () => {
  //      console.log("me diste cick");
    //};

    
//Con Parametro
const handleClick = (message) => {
        console.log(message);
    };
</script>

<template>
  <!--<h1>Hola {{ name.toUpperCase() }}</h1>
  <ul>
    <li v-for="fruta in arrayFrutas">
      {{fruta}}
    </li>
  </ul>-->

  <!--<h1>Hola {{ name.toUpperCase() }}</h1>
  <ul>
    <li v-for="(fruta,index) in arrayFrutas">{{index}} - {{fruta}}  </li>
  </ul>-->

  <h1>Hola {{ name.toUpperCase() }}</h1>
  <ul>
    <li v-for="(fruta,index) in arrayFrutas_0" :key="index">{{index}} - {{fruta}}  </li>
  </ul>

  <h2>{{arrayColores}}</h2>

  <ul>
    <li v-for="fruta in arrayFrutas" :key="fruta.name">{{fruta.name}} - {{fruta.price}} - {{fruta.description}}  </li>
  </ul>

  <ul>
    <li v-for="(value, propiedad, index) in objetoFrutas" :key="index">
          {{index}} - {{propiedad}} - {{value}}  
    </li>
  </ul>

  <!--<h2 v-bind:style="styleColor">Soy azul</h2>
  <h2 :style="styleColor">Soy azul</h2>-->

  <h2 :style="`color: ${arrayColores[2]}`">Soy Perú</h2>

 <!-- <h2> {{activo ? "Estoy activo" : "Estoy inactivo"}} </h2>-->

  <!-- <h2 v-if="activo">Estoy activo</h2>
 <h2 v-if="!activo">Estoy inactivo</h2>-->


  <!--<h2 v-if="activo">Estoy activo</h2>
 <p v-else>Estoy inactivo</p>-->

 <h2 v-if="activo === true">
  <span>Icono</span>
      Estoy activo
  </h2>
 <p v-else-if="activo === false">Estoy inactivo</p>
 <p v-else>Estoy indeciso</p>

  <!--<h2 v-if="activo === true">Estoy activo</h2>
 <p v-else-if="activo === false">Estoy inactivo</p>
 <p v-else>Estoy indeciso</p>-->

 <h2 v-show="activo">Estoy activo v-show</h2>
<br>
<br>
<ul>

   Es posible usarn template dentro de otro templatw-->
    <template v-for="item in arrayFrutas2" :key="item.name">
        <li v-if="item.stock > 0">
            {{ item.name }} - {{ item.price }}
        </li>
    </template>
</ul>

<br>
<br>
<br>
<br>

<button v-on:click="handleClick">Click aquí</button>
    <button @click="handleClick">Click aquí</button>

<br>
<br>

<button v-on:click="handleClick('Texto 1')">Activame 1</button>
<button @click="handleClick('Texto 2')">Activame 2</button>
  

<br>
<br>
<br>


<button @click.right.prevent="handleClick('Texto Right')">
    Click right
</button>

<button @click.middle="handleClick('Texto middle')">
    Click middle
</button>

<button @click="handleClick('Texto left')">
    Click left
</button>

<br>
<br>

<!--
<h2 :class="counter >= 0 ? 'positive' : 'negative'">
        {{ counter }}
    </h2>
    <button @click="increment">Incremet</button>
    <button @click="decrement">Decrement</button>
    <button @click="reset">Reset</button>
-->

<!--
  <h2 :class="classCounter">
        {{ counter }}
    </h2>
  <button @click="increment">Incremet</button>
  <button @click="decrement">Decrement</button>
  <button @click="reset">Reset</button>
  <button @click="add" :disabled="blockNumber">Add</button>
    <ul>
        <li v-for="(item, index) in arrayCounter" :key="index">
            {{ item }}
        </li>
    </ul>
-->

<div class="container text-center mt-5">
        <h1>Hola {{ name }}!</h1>
        <h2 :class="classCounter">
            {{ counter }}
        </h2>

        <div class="btn-group">
            <button @click="increment" class="btn btn-success">Incremet</button>
            <button @click="decrement" class="btn btn-danger">Decrement</button>
            <button @click="reset" class="btn btn-secondary">Reset</button>
            <button
                @click="add"
                :disabled="blockNumber"
                class="btn btn-primary"
            >
                Add
            </button>
        </div>
        <h2 class="mt-3">Mis Favoritos</h2>
        <ul class="list-group mt-2">
            <li
                class="list-group-item"
                v-for="(item, index) in arrayCounter"
                :key="index"
            >
                {{ item }}
            </li>
        </ul>
    </div>



</template>

<style>
h1{
  color: red;
}

.negative {
    color: red;
}

.positive {
    color: green;
}

.zero {
    color: black;
}
</style>