<template>
  <div class="movies__card">
    <div class="card__image">
      <img :src="'https://image.tmdb.org/t/p/original/' + movie.poster_path" alt="Poster" />
    </div>
    <div class="card__title">{{ movie.original_title }}</div>
    <div class="card__rating">{{ movie.vote_average }}/10</div>
    <div class="card__plot">{{ movie.overview.substring(0, 120) }}...</div>
    <div class="card__actions">
      <a href="#" class="btn btn-primary">Details</a>
    </div>
  </div>
</template>

<script setup>
defineProps({
  movie: Object,
});
</script>
