<template>
  <div>
    <h1 id="title">Studio Ghibli Films:</h1>
    <div  class="list-section">
      <film-list-item class="list" :films='films'></film-list-item>
       
    </div>

    <film-detail :film="selectedFilm"></film-detail>
    
      <div id="filterInputYear">
        <h3>Filter Films By Year</h3>
        <input type="number" v-model.number="releaseDate" min="1988" max="2020"/>
      </div>

      <section>
        <ul>
        <li v-for="(film, index) in filteredFilms" :key="index">
          {{ film.title }} 
          {{ film.release_date }}
        </li>
        </ul>
      </section>

       <div id="filterInputDirector">
        <h3>Filter Films By Director</h3>
        <select v-model="filmDirector">
          <option v-for="(film, index) in films" :key="index">{{ film.director }}</option>
        </select>
      </div>

      <section>
        <ul>
        <li v-for="(film, index) in filteredFilmsDirector" :key="index" :film="film">
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
import FilmListItem from './components/FilmListItem.vue'
import { eventBus } from './main';

export default {

  name: 'app',
  data(){
    return {
      films: [],
      selectedFilm: null,
      releaseDate: 1986,
      filmDirector: null,
      directorsList: [],
      
     
    };
  },
  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(results => results.json())
    .then(films => this.films = films)

    // eventBus.$on('film-selected', (film) => {
    //   this.selectedFilm = film
    // })
    eventBus.$on('film-selected', (film) => {
      this.selectedFilm = film
    } )
  },
  computed: {
        filteredFilms: function(){
        return this.films.filter((film) => {
          return film.release_date == this.releaseDate;
        });
      },
        
        filteredFilmsDirector: function(){
        return this.films.filter((film) => {
          return film.director == this.filmDirector;
        });
      },

        filterDirectors: function(){
          return this.films.forEach((film) => {
            this.directorsList.push(film.director);
          });
          
          // let directorsList = [ ...new Set(this.directorsList) ];
          // directorsList.map(director => { return value})
        },

        filterDirectorsMore: function() {
           return this.directorsList = [ ...new Set(this.directorsList) ];
          
        },

        // filterDirectorsNow: function(){        
        // return this.directorsList = [ ...new Set(this.directorsList) ]
        // return this.directorsList.filter((item, index) => this.directorsList.indexOf(item) === item);
        // }

        // filterDirectors: function(film) {
        //   for (director in film.director);
        //   this.directorsList.push(director);
        //   return this.directorsList
        // }
          
        
    },

  methods: {
    //   handleSelect(){
    
    //   ('character-selected', this.selectedCharacter)
    // }
  },
  components: { 
    'films-list': FilmsList,
    'film-detail': FilmDetail,
    'film-director-detail': FilmDirectorDetail,
    'film-list-item': FilmListItem
    
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