<script setup>
import { useRoute } from 'vue-router'
import { ref } from "vue"
//https://router.vuejs.org/guide/essentials/dynamic-matching
const route = useRoute()
const personaje = ref(null)
const loading = ref(true)

fetch("https://dragonball-api.com/api/characters/" + route.params.id)
  .then(res => {
    if( !res.ok ) throw new Error()
    return res.json()
  })
  .then(data => {
    personaje.value = data
  })
  .catch(err => {
    console.log(err)
  })
  .finally(() => {
    loading.value = false
  })

</script>
<template>
  <div v-if="!loading">
    <div v-if="personaje" >
      <h1 class="text-5xl">{{ personaje.name }}</h1>
      <img width="200px" :src="personaje.image" alt="">
      <p>{{ personaje.description }}</p>
    </div>
    <div v-else>
      Error al traer el personaje
    </div>
  </div>
  <div v-else>
    <svg class="size-5 animate-spin text-indigo-500" xmlns="http://w3.org" fill="none" viewBox="0 0 24 24">
      <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
      <path class="opacity-75" fill="currentColor"
        d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z">
      </path>
    </svg>
  </div>
  <RouterLink to="/personajes">Volver</RouterLink>
</template>
