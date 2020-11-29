<template>
  <div>
    <h1 id="title">Studio Ghibli Films:</h1>
    <div  class="list-section">
      <films-list class="list" :films='films'></films-list>
       
    </div>
    <film-detail :film="selectedFilm"></film-detail>
    
      <div id="filterInputYear">
        <h3>Filter Films By Year</h3>
        <input type="number" v-model.number="releaseDate" min="1988" max="2020"/>
      </div>

      <section>
        <ul>
        <li v-for="(film, index) in filteredFilms" :key="index" :film="film">
          {{ film.title }}
          {{ film.release_date }}
        </li>
        </ul>
      </section>

       <div id="filterInputDirector">
        <h3>Filter Films By Director</h3>
        <input type="" v-model="releaseDate" min="1986" max="2020"/>
      </div>

      <section>
        <ul>
        <li v-for="(film, index) in filteredFilms" :key="index" :film="film">
          {{ film.title }}
          {{ film.release_date }}
        </li>
        </ul>
      </section>
    
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
      releaseDate: 2020,
      
     
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
        return this.films.filter((film) => {
          return film.release_date == this.releaseDate;
        });
      }
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
.list {
    display: flex;
    flex-direction: row;
    justify-content: space-between;

  }

/* .list {
  width: 300px;
  margin: 20px;
} */

</style>