<script setup>
import { ref } from "vue"
// https://github.com/public-apis/public-apis
const personajes = ref([])
const links = ref(null)
const current = ref(null)

const fetchApi = (uri = "https://dragonball-api.com/api/characters") => {
  fetch(uri)
    .then(res => res.json())
    .then(data => {
      personajes.value = data.items
      links.value = data.links
      current.value = data.meta.currentPage
    })
    .catch(err => console.log(err))
}
fetchApi()

</script>
<template>
  <h1 class="text-4xl my-3">Personajes</h1>
  <table class="w-full">
    <thead>
      <tr>
        <th>#</th>
        <th>Nombre</th>
        <th>Grupo</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="personaje in personajes">
        <td><img width="50px" :src="personaje.image" alt=""></td>
        <td>{{ personaje.name }}</td>
        <td>{{ personaje.affiliation }}</td>
        <td>
          <RouterLink :to="'/detalle/' + personaje.id" >Ver</RouterLink>
        </td>
      </tr>
    </tbody>
  </table>
  <div class="mt-3 flex space-x-1">
    <button v-show="links?.previous?.length > 0" @click="fetchApi(links.previous)"
      class="rounded-md border border-slate-300 py-2 px-3 text-center text-sm transition-all shadow-sm hover:shadow-lg text-slate-600 hover:text-white hover:bg-slate-800 hover:border-slate-800 focus:text-white focus:bg-slate-800 focus:border-slate-800 active:border-slate-800 active:text-white active:bg-slate-800 disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none ml-2">
      Prev
    </button>
    <button @click="fetchApi('https://dragonball-api.com/api/characters?page=' + current + '&limit=10')"
      class="min-w-9 rounded-md bg-slate-800 py-2 px-3 border border-transparent text-center text-sm text-white transition-all shadow-md hover:shadow-lg focus:bg-slate-700 focus:shadow-none active:bg-slate-700 hover:bg-slate-700 active:shadow-none disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none ml-2">
      {{ current }}
    </button>
    <button @click="fetchApi('https://dragonball-api.com/api/characters?page=' + (parseInt(current) + 1) + '&limit=10')"
      class="min-w-9 rounded-md border border-slate-300 py-2 px-3 text-center text-sm transition-all shadow-sm hover:shadow-lg text-slate-600 hover:text-white hover:bg-slate-800 hover:border-slate-800 focus:text-white focus:bg-slate-800 focus:border-slate-800 active:border-slate-800 active:text-white active:bg-slate-800 disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none ml-2">
      {{ current + 1 }}
    </button>
    <button @click="fetchApi('https://dragonball-api.com/api/characters?page=' + (parseInt(current) + 2) + '&limit=10')"
      class="min-w-9 rounded-md border border-slate-300 py-2 px-3 text-center text-sm transition-all shadow-sm hover:shadow-lg text-slate-600 hover:text-white hover:bg-slate-800 hover:border-slate-800 focus:text-white focus:bg-slate-800 focus:border-slate-800 active:border-slate-800 active:text-white active:bg-slate-800 disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none ml-2">
      {{ current + 2 }}
    </button>
    <button v-show="links?.next?.length > 0" @click="fetchApi(links.next)"
      class="min-w-9 rounded-md border border-slate-300 py-2 px-3 text-center text-sm transition-all shadow-sm hover:shadow-lg text-slate-600 hover:text-white hover:bg-slate-800 hover:border-slate-800 focus:text-white focus:bg-slate-800 focus:border-slate-800 active:border-slate-800 active:text-white active:bg-slate-800 disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none ml-2">
      Next
    </button>
  </div>
</template>
