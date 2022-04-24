<template>
    <div>
        <p class="missingReviews" v-if="ratingNumber == 0" :style="(ratingNumber == 0) ? 'margin-bottom: 0;' : ''">
            Nessuna recensione</p>
        <div id="vote" :style="(ratingNumber == 0) ? 'margin-top: 5px;' : ''">
            <div>
                <font-awesome-icon icon="fa-solid fa-star" v-for="(element,index) in ratingNumber" :key="index" />
            </div>
            <span>{{ratingNumber}}/5</span>
        </div>
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

        .fa-star {
            color: #ffd700;
            margin: 0 1px;
        }

        span {
            margin-left: 7px;
            font-size: 0.9em;
            letter-spacing: 0.2em;
        }
    }

    #vote,
    .missingReviews {
        margin: 20px 0;
    }

    .missingReviews {
        text-decoration: underline;
    }
</style>