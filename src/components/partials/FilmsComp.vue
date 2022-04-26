<template>
    <div id="films">
        <div class="sectionTitle" v-if="foundResults && films.length > 0">
            <h1>film</h1>
            <span>({{films.length}}
                <span class="results" v-if="films.length == 1">risultato</span>
                <span class="results" v-else-if="films.length == 0 || films.length > 1">risultati</span>
                )
            </span>
        </div>

        <div class="selectGenreCont">
            <SelectGenre @selectGenre="selectedGenre"
                v-for="(filmGenre, i) in filmGenres" :key="i" :id="filmGenre.id" :genre="filmGenre.name" />
        </div>


        <div class="containerCards">
            <CardComp v-for="film in filteredFilms" :key="film.id" :title="film.title"
                :language="film.original_language" :vote="film.vote_average" :overview="film.overview"
                :poster="film.poster_path" :genresList="film.genre_ids" :filmGenres="filmGenres" :tvSeriesGenres="tvSeriesGenres"/>
        </div>
    </div>
</template>

<script>
    import CardComp from './CardComp.vue'
    import SelectGenre from './SelectGenre.vue'

    export default {
        name: 'FilmsComp',
        components: {
            CardComp,
            SelectGenre,

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
                return this.films.filter(element => {
                    return element.genre_ids
                        .includes(this.filmGenre[0])
                })
            },

        },

        methods: {
            selectedGenre(text) {
                this.filmGenre = text;

                if (this.filmGenre.length > 0 && !this.checkedFilmsGenres.includes(this.filmGenre[0])) {
                    this.checkedFilmsGenres.push(this.filmGenre[0])
                } else if (this.checkedFilmsGenres.indexOf(this.filmGenre[0]) !== -1) {
                    this.checkedFilmsGenres.slice(this.checkedFilmsGenres.indexOf(this.filmGenre[0]), 1)
                }
            },

        }


    }
</script>

<style lang="scss">
    @import '../../style/global.scss';

    .singleGenre {
        width: 10%;
    }

    .test {
        color: $light-text;
        margin-bottom: 20px;
    }
</style>