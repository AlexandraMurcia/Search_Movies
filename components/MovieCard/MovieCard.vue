<template>
    <Card class="movie-card" @click="showDetails">
      <template  #title>
      </template>
      <template #content>
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Movie Poster" />
      <h3 class="tittle">{{ movie.title }}</h3>
      <h3 class="date" >Lanzamiento: {{ movie.release_date }}</h3>
      </template>
      
    </Card>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  import Card from 'primevue/card'; 
  
  const props = defineProps({
    movie: Object
  });
  const emit = defineEmits(['click']);
  
  function showDetails() {
    emit('click', props.movie);
  }
  </script>

<style src="./MovieCard.scss" scoped></style>
