<template>
    <div id="tvSeries">
        <div class="sectionTitle" v-if="foundResults">
            <h2>series</h2>
            <span>({{tvSeries.length}} risultati)</span>
        </div>

        <div class="containerCards">
            <CardComp v-for="item in tvSeries" :key="item.id" :title="item.name" :language="item.original_language"
                :vote="item.vote_average" :overview="item.overview"/>
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

<style lang="scss">
@import '../../style/global.scss';

    #tvSeries {
        margin-top: 30px;

    }
</style>