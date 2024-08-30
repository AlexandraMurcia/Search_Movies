<template>
  <div>
    <SearchBar @search="fetchMovies" />
    <div v-if="loading" class="loading-indicator">Cargando...</div>
    <div v-else-if="error" class="error-message">{{ error }}</div>
    <div v-else class="movie-grid">
      <MovieCard v-for="movie in movies" :key="movie.id" :movie="movie" @click="selectMovie(movie)" />
    </div>
    <MovieModal v-if="selectedMovie" :movie="selectedMovie" @close="selectedMovie = null" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import SearchBar from '~/components/SearchBar/SearchBar.vue';
import MovieCard from '~/components/MovieCard/MovieCard.vue';
import MovieModal from '~/components/MovieModal/MovieModal.vue';

const movies = ref([]);
const loading = ref(false);
const error = ref(null);
const selectedMovie = ref(null);

async function fetchMovies(query) {
  if (typeof query !== 'string' || !query.trim()) {
    error.value = 'Por favor, ingresa un título de película válido.';
    return;
  }
  loading.value = true;
  error.value = null;
  try {
    const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=8ec142988811c4f39752da4567ed10e9&query=${query}`);
    if (!response.ok) {
      throw new Error('Error al obtener los datos');
    }
    const data = await response.json();
    if (data.results.length === 0) {
      error.value = 'No se encontraron resultados para tu búsqueda.';
    } else {
      movies.value = data.results;
    }
  } catch (err) {
    error.value = 'Hubo un problema con la API. Inténtalo de nuevo más tarde.';
  } finally {
    loading.value = false;
  }
}

function selectMovie(movie) {
  selectedMovie.value = movie;
}
</script>

<style scoped>
.movie-grid {
  display: grid;
    grid-template-columns: repeat(auto-fit, minmax(314px, 1fr));
    gap: 20px;
    margin: 20px;
}
.loading-indicator {
  color: rgb(236, 176, 176);
  text-align: center;
  margin-top: 100px;
  font-size: 30px;
  font-weight: 900;
}
.error-message {
  color: rgb(236, 176, 176);
  text-align: center;
  margin-top: 100px;
  font-size: 30px;
  font-weight: 900;
}
</style>
