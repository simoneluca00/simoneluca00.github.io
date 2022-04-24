<template>
    <div id="films">
        <div class="sectionTitle" v-if="foundResults">
            <h2>film</h2>
            <span>({{films.length}} risultati)</span>
        </div>
        <div class="containerCards">
            <CardComp v-for="film in films" :key="film.id" :title="film.title" :language="film.original_language"
                :vote="film.vote_average" :overview="film.overview" :poster="film.poster_path" />
        </div>
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
            foundResults: Boolean,
        },

        data() {
            return {

            }
        },


    }
</script>

<style lang="scss">
@import '../../style/global.scss';

</style>