<template>
    <div id="tvSeries">
        <div class="sectionTitle" v-if="foundResults">
            <h1>serie tv</h1>
            <span>({{tvSeries.length}} risultati)</span>
        </div>

        <div class="containerCards">
            <CardComp v-for="item in tvSeries" :key="item.id" :title="item.name" :language="item.original_language"
                :vote="item.vote_average" :overview="item.overview" :poster="item.poster_path" />
        </div>
    </div>
</template>

<script>
    import CardComp from './CardComp.vue'

    export default {
        name: 'SeriesComp',
        components: {
            CardComp,
        },

        props: {
            tvSeries: Array,
            foundResults: Boolean,
        },

        data() {
            return {

            }
        },


    }
</script>

<style lang="scss" scoped>
    @import '../../style/global.scss';

    #tvSeries {
        margin-top: 30px;

    }
</style>