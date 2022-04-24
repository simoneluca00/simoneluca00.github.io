<template>
    <div>
        <!-- {{Math.ceil(this.vote / 2 )}} -->
        <font-awesome-icon icon="fa-solid fa-star" v-for="(element,index) in ratingNumber" :key="index"/>
        <p class="missingReviews" v-if="ratingNumber == 0">Nessuna recensione</p>
    </div>
</template>

<script>

  export default {
    name: 'RatingComp',

    props: {
        vote: Number,
    },

    computed:{
        ratingNumber(){
            return Math.ceil(this.vote / 2 );
        },
    }
  }
</script>

<style lang="scss" scoped>
  @import '../../style/global.scss';

  .fa-star {
      color: #ffd700;
  }

  .missingReviews,
  .fa-star {
      margin: 20px 0;
  }

  .missingReviews {
      text-decoration: underline;
  }

</style>