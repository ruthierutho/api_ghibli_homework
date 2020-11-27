<template>
  <div>
    <h1 id="title">Studio Ghibli Films:</h1>
    <div  class="list-section">
      <films-list :films='films'></films-list>
      <film-detail :film="selectedFilm"></film-detail>
    </div>
  </div>
</template>

<script>

import FilmDetail from './components/FilmDetail.vue';
import FilmsList from './components/FilmsList.vue';
import { eventBus } from './main';

export default {

  name: 'app',
  data(){
    return {
      films: [],
      selectedFilm: null,
    };
  },
  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(results => results.json())
    .then(films => this.films = films)

    eventBus.$on('film-selected', (film) => {
      this.selectedFilm = film
    })
  },
  components: { 
    'films-list': FilmsList,
    'film-detail': FilmDetail
    
  },
  

}
</script>

<style>
.list-section {
    display: flex;
    justify-content: space-between;
  }

</style>