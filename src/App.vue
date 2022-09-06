<script setup>
// referencia reactiva
import { ref, computed } from "vue";

const name = "Ejemplo reactivo";
const counter = ref(0);
const arrayFavoritos = ref([]);

/// agregar el value para que se active la reactividad sobre la var counter
const aumentar = () => counter.value++;
const disminuir = () => counter.value--;
const reset = () => (counter.value = 0);

const agregar = () => {
  arrayFavoritos.value.push(counter.value);
};

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "neutro";
  }

  if (counter.value > 0) {
    return "positive";
  }

  if (counter.value < 0) {
    return "negative";
  }
});

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
  if (numSearch === 0) return true; /// evalua el cero porque si no lo encuentra en el array numSearch es igual a cero
  return numSearch ? true : false;
});
</script>

<template>
  <div class="container" style="text-align: center;">
    <h1>{{ name }}!</h1>

    <h2 :class="classCounter">Contar: {{ counter }}</h2>

    <br />

    <button class="btn btn-success" @click="aumentar">Aumentar</button>

    <span> | </span>

    <button class="btn btn-danger" @click="disminuir">Disminuir</button>

    <span> | </span>

    <button class="btn btn-secondary" @click="reset">Reset</button>

    <span> | </span>

    <button class="btn btn-primary" :disabled="bloquearBtnAdd" @click="agregar">
      Agregar favoritos
    </button>

    <br /><br />

    <h2>Lista de numeros favoritos</h2>
    <ul class="list-group">
      <li class="list-group-item" v-for="(item, index) in arrayFavoritos" :key="index">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<style>
.neutro {
  color: black;
}
.negative {
  color: red;
}
.positive {
  color: green;
}
</style>
