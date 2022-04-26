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

                <p class="overview">
                    {{overview}}
                </p>
                <!-- <ul class="singleCardGenre">
                    <li v-for="(genre,i) in associateSeriesGenres" :key="i">{{genre.name}}</li>
                </ul> -->
                <div class="containerGenres">
                    <h4>Generi</h4>
                    <ul class="singleCardGenre">
                        <li v-for="(genre,i) in associateFilmsGenres" :key="i">{{genre.name}}
                            <span v-if="i + 1 < associateFilmsGenres.length">-</span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import RatingComp from './RatingComp.vue';

    export default {
        name: 'CardComp',

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
            foundResults: Boolean,
        },

        computed: {
            removeDuplicateFunction(){
                var uniqueListGenres = this.filmGenres.concat(this.tvSeriesGenres.filter(el => this.filmGenres.every(item => item.id != el.id)));

                return uniqueListGenres
            },
            
            associateFilmsGenres() {

                return this.removeDuplicateFunction.filter((el) => this.genresList.includes(el.id))
            },

            // uniqueListGenres() {
            //     return this.filmGenres.concat(this.tvSeriesGenres)
            // },

        },

        methods: {

        }

    }
</script>

<style lang="scss">
    @import '../../style/global.scss';

    @import url('https://fonts.googleapis.com/css2?family=Yanone+Kaffeesatz:wght@400;500;600;700&display=swap');

    .border-card {
        border: 2px solid;
        border-image-slice: 1;
        border-image-source: $br-cards;
    }

    .flip-card {
        background-color: transparent;
        height: 300px;
        perspective: 1000px;
        cursor: pointer;

        &:hover .flip-card-inner {
            transform: rotateY(180deg);
        }
    }

    .flip-card-inner {
        position: relative;
        @include w-h-100;
        text-align: center;
        transition: transform 0.8s;
        transform-style: preserve-3d;

        h2 {
            font-family: 'Yanone Kaffeesatz', sans-serif;
            font-size: 1.8em;
        }
    }

    .flip-card-front,
    .flip-card-back {
        position: absolute;
        @include w-h-100;
        -webkit-backface-visibility: hidden;
        backface-visibility: hidden;
    }

    .flip-card-front {
        background-color: transparent;

        img {
            @include w-h-100;
        }

        div.missingPoster {
            @include w-h-100;
            @include compileFlex(center, center);
            background-color: $black;
            color: $light-text;
        }
    }

    .flip-card-back {
        background-color: $black;
        color: $light-text;
        overflow-y: auto;
        padding: 20px 10px;
        transform: rotateY(180deg);

        img {
            vertical-align: middle;
            width: 18px;
            height: 14px;
        }

        h2 {
            margin-bottom: 20px;
        }

        p {
            margin: 10px 0;
        }

        .overview {
            padding: 0 7px 0 20px;
            text-align: start;
            line-height: 1.4em;
        }

        .containerGenres {
            margin-top: 10px;
            padding-top: 5px;
            border-top: 1px solid $light-text;

            h4 {
                margin-bottom: 10px
            }

            .singleCardGenre {
                @include compileFlex(center, center);
                flex-wrap: wrap;
                list-style-type: none;
    
                li {
                    width: auto;
                    margin-bottom: 5px;

                    span {
                        margin: 0 5px 0 2px;
                    }
                }
            }
        }

    }

    .flip-card-back::-webkit-scrollbar {
        width: 10px;
    }

    .flip-card-back::-webkit-scrollbar-track {
        background: $black;
    }

    .flip-card-back::-webkit-scrollbar-thumb {
        background-color: $primary-logo;
        border-radius: 16px;
        border: 3px solid $black;
    }
</style>