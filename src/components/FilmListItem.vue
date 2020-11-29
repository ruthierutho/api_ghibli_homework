<template>
  <!-- <li v-on:click="handleClick">{{film.title}}</li> -->
    <div>
    <select v-on:change="handleSelect" v-model="selectedFilm">
      <option disabled value="">Select a film...</option>
      <option v-for="(film, index) in films" :key="index" :value="film">{{film.title}}</option>
    </select>
    </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
    name: 'film-list-item',
    props: ['films'],
    methods: {
        // handleClick() {
        //     eventBus.$emit('film-selected', this.film)
        // }
        handleSelect() {
            eventBus.$emit('film-selected', this.selectedFilm)
        }
    }


}
</script>

<style>

</style>