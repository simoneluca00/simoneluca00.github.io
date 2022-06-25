<template>
    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front" :class="(poster == null) ? 'border-card': ''">
                <div class="missingPoster" v-if="poster == null">
                    <h2>{{title}}</h2>
                </div>
                <img v-else :src="`https://image.tmdb.org/t/p/w342${poster}`" :alt="`Copertina di “${title}“`">
            </div>

            <div class="flip-card-back border-card">
                <h2 v-if="poster != null">{{title}}</h2>
                <div>Lingua originale:
                    <img src="../../assets/img/it.png" alt="Italian flag" v-if="language == 'it'">
                    <img src="../../assets/img/en.png" alt="English flag" v-else-if="language == 'en'">
                    <img src="../../assets/img/es.png" alt="Spanish flag" v-else-if="language == 'es'">
                    <img src="../../assets/img/fr.png" alt="French flag" v-else-if="language == 'fr'">
                    <img src="../../assets/img/de.png" alt="German flag" v-else-if="language == 'de'">
                    <img src="../../assets/img/zh.png" alt="Chinese flag" v-else-if="language == 'zh'">
                    <img src="../../assets/img/hi.png" alt="Indian flag" v-else-if="language == 'hi'">
                    <img src="../../assets/img/tr.png" alt="Turkish flag" v-else-if="language == 'tr'">
                    <img src="../../assets/img/pt.png" alt="Portuguese flag" v-else-if="language == 'pt'">
                    <strong v-else>{{language}}</strong>
                </div>

                <RatingComp :vote="vote" />

                <p class="overview text-start">
                    {{overview}}
                </p>

                <div class="divisor"></div>
                <div class="containerGenres">
                    <h4>Generi</h4>
                    <ul class="singleCardGenre">
                        <li v-for="(genre,i) in associateFilmsGenres" :key="i">{{genre.name}}
                            <span v-if="i + 1 < associateFilmsGenres.length">-</span>
                        </li>

                        <li v-if="associateFilmsGenres.length == 0">Nessun genere corrispondente per questo elemento :(
                        </li>
                    </ul>
                </div>

                <div class="divisor"></div>

                <div class="containerActors">
                    <h4>Attori</h4>
                    <p>{{sliceTvActors()}}</p>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import RatingComp from './childComps/RatingComp.vue';

    export default {
        name: 'CardSeries',

        components: {
            RatingComp,
        },

        props: {
            title: String,
            language: String,
            vote: Number,
            overview: String,
            poster: String,
            genresList: Array,
            tvSeriesGenres: Array,
            filmGenres: Array,
            seriesId: Number,
            propsApiKey: String,
            foundResults: Boolean,

        },

        data() {
            return {
                tvActorsArray: [],
            }
        },

        mounted() {


            axios.get(`https://api.themoviedb.org/3/tv/${this.seriesId}/credits?api_key=${this.propsApiKey}`)
                .then((resTV) => {
                    this.tvActorsArray = resTV.data.cast;
                })
                .catch(err => console.error('Impossibile caricare i dati', err));
        },

        computed: {
            removeDuplicateFunction() {
                return this.filmGenres.concat(this.tvSeriesGenres.filter(el => this.filmGenres.every(item => item.id !=
                    el.id)));
            },

            associateFilmsGenres() {
                return this.removeDuplicateFunction.filter((el) => this.genresList.includes(el.id));
            },

            movieActorsToPrint(){
               return this.tvActorsArray.map(element => {
                    return element.original_name
                });
            }

        },

        methods: {

            sliceTvActors(){
                var fiveTvActors = this.movieActorsToPrint.slice(0,5).join(' - ');
                return fiveTvActors
            },
        }

    }
</script>

<style lang="scss">
    // @import '../../style/global.scss';
</style>