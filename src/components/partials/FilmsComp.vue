<template>
    <div id="films">
        <div class="sectionTitle">
            <h2>films</h2>
            <span>({{films.length}} risultati)</span>
        </div>
        <ul>
            <CardComp v-for="film in films" :key="film.id" :title="film.title" :language="film.original_language"
                :vote="film.vote_average" :overview="film.overview"/>
        </ul>
    </div>
</template>

<script>
    import CardComp from './CardComp.vue'

    export default {
        name: 'FilmsComp',
        components: {
            CardComp,
        },

        props: {
            films: Array,
        },

        data() {
            return {

            }
        },


    }
</script>

<style lang="scss">

    ul {
        list-style-type: none;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }
</style>