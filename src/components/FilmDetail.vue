<template>
    <div>
        <h4>{{ film.title }}</h4>
        <p>{{ film.release_date }}</p>
        <p>{{ film.director }}</p>
    </div>
</template>

<script>
export default {
    name: 'film-detail',
    props: ['film'],

}
</script>

<style>

</style>