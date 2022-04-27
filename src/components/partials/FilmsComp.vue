<template>
    <div id="films">
        <div class="sectionTitle" v-if="foundResults && films.length > 0">
            <h1>film</h1>
            <span>({{filteredFilms.length}}
                <span class="results" v-if="filteredFilms.length == 1">risultato</span>
                <span class="results" v-else-if="filteredFilms.length == 0 || filteredFilms.length > 1">risultati</span>
                )
            </span>
        </div>

        <CheckFilmComp @selectGenre="selectedGenre" :filmGenres="filmGenres" />

        <div v-if="foundResults && filteredFilms.length == 0">
            <h2 class="noGenreResults">Non sono presenti Film corrispondenti al genere selezionato</h2>
        </div>

        <div class="containerCards">
            <CardComp v-for="film in filteredFilms" :key="film.id" :title="film.title"
                :language="film.original_language" :vote="film.vote_average" :overview="film.overview"
                :poster="film.poster_path" :genresList="film.genre_ids" :filmGenres="filmGenres" 
                :tvSeriesGenres="tvSeriesGenres"/>
        </div>
    </div>
</template>

<script>
    import CardComp from './CardComp.vue'
    import CheckFilmComp from './childComps/CheckFilmComp.vue'

    export default {
        name: 'FilmsComp',
        components: {
            CardComp,
            CheckFilmComp,

        },

        props: {
            films: Array,
            filmGenres: Array,
            tvSeriesGenres: Array,
            foundResults: Boolean,
        },

        data() {
            return {
                filmGenre: "",
            }
        },

        computed: {

            filteredFilms() {
                if (this.filmGenre == "") {
                    return this.films
                }

                return this.films.filter((element) => {
                    return this.filmGenre
                        .every((item)=> element.genre_ids.includes(item))

                })
            },

        },

        methods: {
            selectedGenre(text) {
                this.filmGenre = text;
            },

        }


    }
</script>

<style lang="scss">
    @import '../../style/global.scss';

    #films {
        min-height: 50vh;

        h2.noGenreResults {
            color: #fff;
        }
    }

</style>