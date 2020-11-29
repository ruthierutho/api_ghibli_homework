<template>
    <div v-if='film'>
        <h4>{{ film.title }}</h4>
        <p>{{ film.release_date }}</p>
        <p>{{ film.director }}</p>
        <p id="description">{{ film.description }}</p>
    </div>
</template>

<script>
export default {
    name: 'film-detail',
    props: ['film'],

}
</script>

<style >
#description {
    width: 20%;
}


</style>