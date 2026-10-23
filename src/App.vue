<script setup>
import { RouterLink } from 'vue-router';

</script>
<template>
  <header>
    <nav>
      <ul>
        <li><RouterLink to="/">Home V2</RouterLink></li>
        <li><RouterLink to="/personajes">Personajes</RouterLink></li>
        <li><RouterLink to="/contact">Contacto</RouterLink></li>
      </ul>
    </nav>
  </header>
  <RouterView></RouterView>
  <footer></footer>
</template>
