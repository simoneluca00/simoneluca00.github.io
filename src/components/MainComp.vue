<template>
  <main>
    <FilmsComp :films="films" :foundResults="foundResults" />

    <SeriesComp :tvSeries="tvSeries" :foundResults="foundResults" />
  </main>
</template>

<script>
  import FilmsComp from './partials/FilmsComp.vue'
  import SeriesComp from './partials/SeriesComp.vue'

  export default {
    name: 'MainComp',

    components: {
      FilmsComp,
      SeriesComp,
    },

    props: {
      films: Array,
      tvSeries: Array,
      foundResults: Boolean,
    },

    methods: {
      wela(){
        for (let i = 0; i < this.films.length; i++) {
          console.log(this.films.vote_average)
          
        }
      }
    }
  }
</script>

<style lang="scss">
  @import '../style/global.scss';

  main {
    background-color: $main-gray;
    min-height: 90vh;
    padding: 20px 0;
    font-family: sans-serif;

    div.sectionTitle {
      @include compileFlex (center, initial);
      color: $white;
      padding: 10px 0;
      margin-bottom: 20px;


      h1 {
        text-transform: uppercase;
        text-align: center;

      }

      span {
        font-size: 0.9em;
        font-weight: bold;
        align-self: flex-end;
        margin-bottom: 4px;
        margin: 0 0 7px 4px;
      }
    }

    .containerCards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 20%));
      max-width: 85%;
      margin: 0 auto;
      // gap: 20px;
      color: $white;
    }

  }

  @media screen and (max-width: 490px) {
    .containerCards {
      width: 270px;
    }
    
  }
</style>