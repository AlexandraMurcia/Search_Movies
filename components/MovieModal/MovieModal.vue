<template>
    <Dialog v-model:visible="visible" class="movie-modal custom-dialog" :header="movie.title" modal>
      <div class="modal-content">
        <div class="poster">
          <img class="image" :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Movie Poster" />
        </div>
        
        <div class="info">
        <h3 class="overview">{{ movie.overview }}</h3>
        <h3 class="date">Fecha de lanzamiento: {{ movie.release_date }}</h3>
        <h3 class="vote">Calificación: {{ movie.vote_average }}</h3>
      </div>
      </div>
    </Dialog>
  </template>
  
  <script setup>
  import { defineProps, defineEmits, ref, watch } from 'vue';
  import Dialog from 'primevue/dialog';
  import Button from 'primevue/button';
  
  const props = defineProps({
    movie: Object
  });
  const emit = defineEmits(['close']);
  const visible = ref(false);
  
  watch(() => props.movie, (newVal) => {
    visible.value = !!newVal;
  });
  
  function close() {
    visible.value = false;
    emit('close');
  }
  </script>
  
  <style src="./MovieModal.scss" scoped></style>
  