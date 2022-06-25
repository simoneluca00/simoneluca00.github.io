<template>
    <div id="tvSeries">
        <div class="sectionTitle" v-if="foundResults && tvSeries.length > 0">
            <h1>serie tv</h1>
            <span>({{filteredSeries.length}}
                <span class="results" v-if="filteredSeries.length == 1">risultato</span>
                <span class="results"
                    v-else-if="filteredSeries.length == 0 || filteredSeries.length > 1">risultati</span>
                )
            </span>
        </div>

        <CheckSeriesComp @selectGenre="selectedGenre" :tvSeriesGenres="tvSeriesGenres" />

        <div v-if="foundResults && filteredSeries.length == 0">
            <h2 class="noGenreResults">Non sono presenti Serie Tv corrispondenti al genere selezionato</h2>
        </div>

        <div class="containerCards">
            <CardSeries v-for="item in filteredSeries" :key="item.id" :title="item.name"
                :language="item.original_language" :vote="item.vote_average" :overview="item.overview"
                :poster="item.poster_path" :genresList="item.genre_ids" :tvSeriesGenres="tvSeriesGenres"
                :filmGenres="filmGenres" :seriesId="item.id" :propsApiKey="propsApiKey"/>
        </div>
    </div>
</template>

<script>
    import CardSeries from './CardSeries.vue'
    import CheckSeriesComp from './childComps/CheckSeriesComp.vue'

    export default {
        name: 'SeriesComp',
        components: {
            CardSeries,
            CheckSeriesComp,

        },

        props: {
            tvSeries: Array,
            tvSeriesGenres: Array,
            filmGenres: Array,
            foundResults: Boolean,
            propsApiKey: String,
        },

        data() {
            return {
                tvSeriesGenre: "",
            }
        },

        computed: {
            filteredSeries() {
                if (this.tvSeriesGenre == "") {
                    return this.tvSeries
                }
                return this.tvSeries.filter(element => {
                    return this.tvSeriesGenre
                        .every((item)=> element.genre_ids.includes(item))
                })
            },

        },

        methods: {
            selectedGenre(text) {
                this.tvSeriesGenre = text;
            }
        }
    }
</script>

<style lang="scss">
    @import '../../style/global.scss';

    #tvSeries {
        margin-top: 100px;
        min-height: 50vh;

        h2.noGenreResults {
            color: $black;
        }
    }
</style>