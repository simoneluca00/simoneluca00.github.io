<template>
    <div id="vote">
        <p class="missingReviews" v-if="ratingNumber == 0">
            Nessuna recensione
        </p>
        <div>
            <font-awesome-icon icon="fa-solid fa-star" v-for="(element,index) in ratingNumber" :key="index" />
            <font-awesome-icon icon="fa-regular fa-star" v-for="(element,index) in (5 - ratingNumber)" :key="'a'+index" />
        </div>
        <span>{{ratingNumber}}/5</span>
    </div>
</template>

<script>
    export default {
        name: 'RatingComp',

        props: {
            vote: Number,
        },

        computed: {
            ratingNumber() {
                return Math.ceil(this.vote / 2);
            },
        }
    }
</script>

<style lang="scss" scoped>
    @import '../../style/global.scss';

    #vote {
        @include compileFlex(center, center);
        flex-direction: column;
        margin: 20px 0;

        .fa-star {
            color: #ffd700;
            margin: 0 1px;
        }

        span {
            margin-top: 5px;
            font-size: 0.9em;
            letter-spacing: 0.2em;
        }
    }

    // #vote,
    // .missingReviews {
    // }

    .missingReviews {
        text-decoration: underline;
    }
</style>