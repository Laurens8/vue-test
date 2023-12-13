<template>
  <section class="section__movies">
    <div class="container">
      <div class="row">
        <div class="col">
          <div class="movies__header">
            <h2 class="header__title">Movies</h2>
            <div class="header__search"><input type="text" v-model="searchText" placeholder="Search" /></div>
          </div>
        </div>
      </div>
      <div class="row g-3" v-if="!loading">
        <div class="col-md-4" v-for="movie in filteredMovies" :key="movie.id">
          <MovieCard :movie="movie" />
        </div>
      </div>
      <div class="row" v-else-if="error">
        <div class="col">Kan films niet laden!</div>
      </div>
      <div class="row" v-else>
        <div class="col">Loading...</div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref, computed } from 'vue';
import MovieCard from './MovieCard.vue';

const movies = ref([]);
const searchText = ref('');

const url = 'https://api.themoviedb.org/3/movie/popular?api_key=4c3890a25990466f04b6e90464c902fd';
const loading = ref(true);
const error = ref(null);

onMounted(async () => {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error('Failed to fetch data');
    }
    const data = await response.json();
    movies.value = data.results;
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
});

const filteredMovies = computed(() => {
  const search = searchText.value.toLowerCase();
  return movies.value.filter((movie) => {
    return movie.title.toLowerCase().includes(search);
  });
});
</script>
