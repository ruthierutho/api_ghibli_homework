<template>
  <div>
    <h1 id="title">Studio Ghibli Films:</h1>
    <div  class="list-section">
      <films-list :films='films'></films-list>
    </div>
  </div>
</template>

<script>
import FilmsList from './components/FilmsList.vue';
export default {
  components: { 
    'films-list': FilmsList
  },
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
  }
  

}
</script>

<style>

</style>