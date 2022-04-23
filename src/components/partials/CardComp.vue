<template>
    <li class="card">
        <p>Titolo:
            <strong>{{title}}</strong>     
        </p>
        <p>Lingua originale:
            <strong>{{language}}</strong>          
        </p>
        <p>Voto:
            <strong>{{vote}}</strong>          
        </p>

        <p>
            <strong>{{overview}}</strong>          
        </p>
    </li>
</template>

<script>
    export default {
        name: 'CardComp',

        props: {
            title: String,
            language: String,
            vote: Number,
            overview: String,
        },

        data() {
            return {

            }
        },


    }
</script>

<style lang="scss">
    li {
        border: 1px solid red;
        width: calc((100% / 5 - 40px));
        margin: 10px 20px;
        text-align: center;
        height: 200px;
        overflow-y: auto;

        p {
            margin: 10px 0;
        }
    }
</style>