<template>
  <div>
    <h1 id="title">Studio Ghibli Films:</h1>
  </div>
</template>

<script>
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
  }
  

}
</script>

<style>

</style>