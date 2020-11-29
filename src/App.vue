<template>
  <div>
    <h1 id="title">Studio Ghibli Films:</h1>
    <div  class="list-section">
      <films-list class="list" :films='films'></films-list>
      <film-detail :film="selectedFilm"></film-detail>
       
    </div>
    
     
     <!-- <film-director-detail :filmDirector="filmDirector" :films="films"></film-director-detail> -->
  </div>
</template>

<script>

import FilmDetail from './components/FilmDetail.vue';
import FilmDirectorDetail from './components/FilmDirectorDetail.vue';
import FilmsList from './components/FilmsList.vue';
import { eventBus } from './main';

export default {

  name: 'app',
  data(){
    return {
      films: [],
      selectedFilm: null,
      filmDirector: null,
      
     
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
  computed: {
        filteredFilms: function(){
        return this.films.filter((account) => {
          return account.balance >= this.filmDirector;
        });
      }
    },
  

  },
  methods: {
      handleSelect(){
    
      ('character-selected', this.selectedCharacter)
    }
  },
  components: { 
    'films-list': FilmsList,
    'film-detail': FilmDetail,
    'film-director-detail': FilmDirectorDetail
    
  },
  

}
</script>

<style>
/* .list-section {
    display: flex;
    flex-direction: row;
    justify-content: space-between;

  } */

/* .list {
  width: 300px;
  margin: 20px;
} */

</style>