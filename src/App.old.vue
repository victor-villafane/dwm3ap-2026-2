<script setup>
import { ref } from "vue"
const mensaje = 'Hola soy una variable!'

const personajes = ['Homero', 'Marge', 'Lisa', 'Bart', 'Maggie']
const contador = ref(0)
const click = () => {
  // contador++ // -> Asi no va a funcionar
  contador.value++
}
</script>

<template>
  <h1>{{ contador }}</h1>
  <ul>
    <li v-for="personaje in personajes">
      <span @click="click">{{ personaje }}</span>
    </li>
  </ul>
</template>

<style scoped></style>
