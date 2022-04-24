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
                <h2>{{title}}</h2>
                <div>Lingua originale:
                    <img src="../../assets/img/it.png" alt="Italy flag" v-if="language == 'it'">
                    <img src="../../assets/img/gb.png" alt="UK flag" v-else-if="language == 'en'">
                    <strong v-else>{{language}}</strong>          
                </div>

                <RatingComp :vote="vote"/>
                <!-- <p>Voto:
                    <strong>{{Math.ceil(vote)/2}}</strong> 

                </p> -->

                <p class="overview">
                    {{overview}}          
                </p>
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
            foundResults: Boolean,
        },

    }
</script>

<style lang="scss" scoped>
@import '../../style/global.scss';

@import url('https://fonts.googleapis.com/css2?family=Yanone+Kaffeesatz:wght@400;500;600;700&display=swap');

    .border-card {
        border: 2px solid $primary-red;
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
            @include compileFlex(center,center);
            background-color: $black;
            color: $white;
        }
    }

    .flip-card-back {
        background-color: $black;
        color: $white;
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
            padding:0 7px 0 20px;
            text-align: start;
            line-height: 1.4em;
        }
    }

    .flip-card-back::-webkit-scrollbar{
        width: 10px;
    }

    .flip-card-back::-webkit-scrollbar-track {
        background: $black;        
    }

    .flip-card-back::-webkit-scrollbar-thumb {
        background-color: $main-gray;
        border-radius: 16px;
        border: 3px solid $black;
    }

</style>