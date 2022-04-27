<template>
<ul>
    <li class="singleGenre" v-for="(item, i) in tvSeriesGenres" :key="i">
        <input type="checkbox" :value="item.id" v-model="checkedGenre" @change="$emit( 'selectGenre', checkedGenre)">
        <label :for="item.name">{{item.name}}</label>
    </li>
</ul>
</template>

<script>
    export default {
        name: 'CheckFilmComp',
        props: {
            tvSeriesGenres: Array,
        },
        data() {
            return {
                checkedGenre: [],
            };
        },
    };
</script>

<style lang="scss" scoped>
    @import '../../../style/global.scss';

    ul {
        display: flex;
        flex-wrap: wrap;

        .singleGenre {
            @include compileFlex(center, center);
            flex-direction: column;
            width: calc(100% / 8);
            margin-bottom: 30px;

    
            input {
                margin-bottom: 5px;
            }
    
            label {
                color: $light-text;
                text-transform: uppercase;
                font-size: 0.9em;
            }
        }
    }

</style>