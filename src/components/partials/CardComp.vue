<template>
    <!-- <div class="card">
        <div class="card-inner">
            <div class="card-front">
                <p>Titolo:
                    <strong>{{title}}</strong>     
                </p>
                <div>Lingua originale:
                    <img src="../../assets/img/it.png" alt="Italy flag" v-if="language == 'it'">
                    <img src="../../assets/img/gb.png" alt="UK flag" v-else-if="language == 'en'">
                    <strong v-else>{{language}}</strong>          
                </div>
                <p>Voto:
                    <strong>{{vote}}</strong>          
                </p>

                <p class="overview">
                    {{overview}}          
                </p>
            </div>

            <div class="card-back">

            </div>
        </div>
            
    </div> -->
    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <img :src="`https://image.tmdb.org/t/p/w342${poster}`" :alt="`Copertina '${title}'`">
            </div>

            <div class="flip-card-back">
                <p>Titolo:
                    <strong>{{title}}</strong>     
                </p>
                <div>Lingua originale:
                    <img src="../../assets/img/it.png" alt="Italy flag" v-if="language == 'it'">
                    <img src="../../assets/img/gb.png" alt="UK flag" v-else-if="language == 'en'">
                    <strong v-else>{{language}}</strong>          
                </div>
                <p>Voto:
                    <strong>{{vote}}</strong>          
                </p>

                <p class="overview">
                    {{overview}}          
                </p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'CardComp',

        props: {
            title: String,
            language: String,
            vote: Number,
            overview: String,
            poster: String,
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

    .flip-card {
        background-color: transparent;
        height: 300px;
        border: 2px solid $primary-red;
        perspective: 1000px;
        cursor: pointer;
        
        &:hover .flip-card-inner {
            transform: rotateY(180deg);
        }
    }

    .flip-card-inner {
        position: relative;
        width: 100%;
        height: 100%;
        text-align: center;
        transition: transform 0.8s;
        transform-style: preserve-3d;
    }

    .flip-card-front,
    .flip-card-back {
        position: absolute;
        width: 100%;
        height: 100%;
        -webkit-backface-visibility: hidden;
        backface-visibility: hidden;
    }

    .flip-card-front {
        @include compileFlex(center,center);

        background-color: transparent;

        
        img {
            width: 100%;
            height: 100%;
            line-height: 300px;
            text-decoration: underline;
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

        p {
            margin: 10px 0;
        }

        .overview {
            padding:0 7px 0 20px;
            text-align: start;
            line-height: 1.4em;
        }
    }

</style>