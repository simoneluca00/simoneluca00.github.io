<template>
    <div class="card">
        <p>Titolo:
            <strong>{{title}}</strong>     
        </p>
        <div>Lingua originale:
            <!-- <strong>{{language}}</strong>           -->
            <img src="../../assets/img/it.png" alt="Italy flag" v-if="language == 'it'">
            <img src="../../assets/img/gb.png" alt="UK flag" v-else-if="language == 'en'">
        </div>
        <p>Voto:
            <strong>{{vote}}</strong>          
        </p>

        <p class="overview">
            {{overview}}          
        </p>
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

    .card {
        border: 1px solid red;
        text-align: center;
        height: 300px;
        overflow-y: auto;
        background-color: $black;

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