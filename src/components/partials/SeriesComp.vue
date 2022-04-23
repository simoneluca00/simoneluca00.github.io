<template>
    <div id="tvSeries">
        <div class="sectionTitle">
            <h2>series</h2>
            <span>({{tvSeries.length}} risultati)</span>
        </div>

        <ul>
            <CardComp v-for="item in tvSeries" :key="item.id" :title="item.name" :language="item.original_language"
                :vote="item.vote_average" :overview="item.overview"/>
        </ul>
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
        },

        data() {
            return {

            }
        },


    }
</script>

<style lang="scss">
    #tvSeries {
        margin-top: 30px;

        ul {
            list-style-type: none;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
        }
    }
</style>