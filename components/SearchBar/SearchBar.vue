<template>
    <div class="tittle">
            Busca tu pelicula favorita
        </div>
    <div class="search-bar">
      <InputText class="inputText" v-model="query" placeholder="Buscar películas..." @keyup.enter="searchMovies" />
      <Button class="button" icon="pi pi-search" @click="searchMovies" />
    </div>
  </template>
  
  <script setup>
  import { ref, defineEmits } from 'vue';
  
  const query = ref('');
  const emit = defineEmits(['search']);
  
  function searchMovies() {
  emit('search', query.value);
}
  </script>

<style src="./SearchBar.scss" scoped></style>
