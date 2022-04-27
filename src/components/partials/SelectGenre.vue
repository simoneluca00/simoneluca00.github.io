<template>
    <div class="singleGenre">
        <label :for="genre">{{genre}}
            <input type="checkbox" :value="id" v-model="checkedGenre" @change="$emit( 'selectGenre', checkedGenre)">
        </label>
    </div>
</template>

<script>
    export default {
        name: 'SelectGenre',
        props: {
            id: Number,
            genre: String,
        },
        data() {
            return {
                checkedGenre: [],
            };
        },
    };
</script>

<style lang="scss" scoped>
    @import '../../style/global.scss';

    .singleGenre {
        margin-bottom: 30px;

        label {
        @include compileFlex(center, center);
            flex-direction: column-reverse;
            color: $light-text;
            text-transform: uppercase;
            font-size: 0.9em;

            input {
                margin-bottom: 5px;
            }
        }
    }

</style>