<template>
    <div v-if="filmDirector === this.film.director">
        <h4>{{ film.director }}</h4>
        <ul>
        <li v-for="(film, index) in films" :key="index" :films="films">
            {{film.name}}
        </li>
        </ul>
      
    </div>
</template>

<script>
export default {
    name: 'film-director-detail',
    props: ['films', 'filmDirector'],


}
</script>

<style >


</style>