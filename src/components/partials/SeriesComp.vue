<template>
    <div id="tvSeries">
        <div class="sectionTitle" v-if="foundResults && tvSeries.length > 0">
            <h1>serie tv</h1>
            <span>({{tvSeries.length}}
                <span class="results" v-if="tvSeries.length == 1">risultato</span>
                <span class="results" v-else-if="tvSeries.length == 0 || tvSeries.length > 1">risultati</span>
                )
            </span>
        </div>

        <div class="selectGenreCont">
            <SelectGenre :checkedSeriesGenres="checkedSeriesGenres" @selectGenre="selectedGenre"
                v-for="(tvSeriesGenre, i) in tvSeriesGenres" :key="i" :id="tvSeriesGenre.id"
                :genre="tvSeriesGenre.name" />
        </div>

        <div class="containerCards">
            <CardComp v-for="item in filteredSeries" :key="item.id" :title="item.name"
                :language="item.original_language" :vote="item.vote_average" :overview="item.overview"
                :poster="item.poster_path" :genresList="item.genre_ids" />
        </div>
    </div>
</template>

<script>
    import CardComp from './CardComp.vue'
    import SelectGenre from './SelectGenre.vue'

    export default {
        name: 'SeriesComp',
        components: {
            CardComp,
            SelectGenre,

        },

        props: {
            tvSeries: Array,
            tvSeriesGenres: Array,
            foundResults: Boolean,
        },

        data() {
            return {
                checkedSeriesGenres: [],
                tvSeriesGenre: "",
            }
        },

        computed: {
            filteredSeries() {
                if (this.tvSeriesGenre == "") {
                    return this.tvSeries
                }
                return this.tvSeries.filter(element => {
                    return element.genre_ids
                        .includes(this.tvSeriesGenre[0])
                })
            },

        },

        methods: {
            selectedGenre(text) {
                this.tvSeriesGenre = text;
                if (this.tvSeriesGenre.length > 0 && !this.checkedSeriesGenres.includes(this.tvSeriesGenre[0])) {
                        this.checkedSeriesGenres.push(this.tvSeriesGenre[0])
                } else if (this.checkedSeriesGenres.indexOf(this.tvSeriesGenre[0]) !== -1){
                    this.checkedSeriesGenres.slice(this.checkedSeriesGenres.indexOf(this.tvSeriesGenre[0]),1)
                }
            }
        }
    }

</script>

<style lang="scss">
    @import '../../style/global.scss';

    #tvSeries {
        margin-top: 100px;

        .singleGenre {
            width: calc(100% / 8);
        }
    }
</style>