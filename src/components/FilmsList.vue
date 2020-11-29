<template>
    <div>
        <ul>
            <film-list-item v-for="(film, index) in films" :film='film' :key='index'></film-list-item>
        </ul>
    </div>
</template>

<script>
import FilmListItem from './FilmListItem.vue'
export default {
    name: 'films-list',
    props: ['films'],
  components: { 
      'film-list-item': FilmListItem },

}
</script>

<style>

</style>