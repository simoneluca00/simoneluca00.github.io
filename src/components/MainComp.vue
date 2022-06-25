<template>
  <main>
    <FilmsComp :films="films" :foundResults="foundResults" :filmGenres="filmGenres" :tvSeriesGenres="tvSeriesGenres"
      :propsApiKey="propsApiKey" />

    <SeriesComp :tvSeries="tvSeries" :foundResults="foundResults" :tvSeriesGenres="tvSeriesGenres"
      :filmGenres="filmGenres" :propsApiKey="propsApiKey" />
  </main>
</template>

<script>
  import FilmsComp from './partials/FilmsComp.vue'
  import SeriesComp from './partials/SeriesComp.vue'

  export default {
    name: 'MainComp',

    components: {
      FilmsComp,
      SeriesComp
    },

    props: {
      films: Array,
      tvSeries: Array,
      foundResults: Boolean,
      filmGenres: Array,
      tvSeriesGenres: Array,
      propsApiKey: String,
    },

    computed: {

    },

  }
</script>

<style lang="scss">
  @import '../style/global.scss';
  @import url('https://fonts.googleapis.com/css2?family=Yanone+Kaffeesatz:wght@400;500;600;700&display=swap');

  main {
    background-image: $bg-main;
    min-height: 90vh;
    padding: 20px 0;
    font-family: sans-serif;

    div.sectionTitle {
      @include compileFlex (center, initial);
      color: $light-text;
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

      .results {
        margin-left: -1px;
      }
    }

    .containerCards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 20%));
      max-width: 85%;
      margin: 0 auto;
      // gap: 20px;
      color: $light-text;
    }

    div.selectGenreCont {
      @include compileFlex(flex-start, center);
      flex-wrap: wrap;
    }

    h2.noGenreResults {
      text-align: center;
      margin-top: 100px;
    }


    .border-card {
      border: 2px solid;
      border-image-slice: 1;
      border-image-source: $br-cards;
    }

    .text-start {
      text-align: start;
    }

    .flip-card {
      background-color: transparent;
      height: 300px;
      perspective: 1000px;
      cursor: pointer;

      &:hover .flip-card-inner {
        transform: rotateY(180deg);
      }
    }

    .flip-card-inner {
      position: relative;
      @include w-h-100;
      text-align: center;
      transition: transform 0.8s;
      transform-style: preserve-3d;

      h2 {
        font-family: 'Yanone Kaffeesatz', sans-serif;
        font-size: 1.8em;
      }
    }

    .flip-card-front,
    .flip-card-back {
      position: absolute;
      @include w-h-100;
      -webkit-backface-visibility: hidden;
      backface-visibility: hidden;
    }

    .flip-card-front {
      background-color: transparent;

      img {
        @include w-h-100;
      }

      div.missingPoster {
        @include w-h-100;
        @include compileFlex(center, center);
        background-color: $black;
        color: $light-text;

        h2 {
          max-width: 80%;
        }
      }
    }

    .flip-card-back {
      background-color: $black;
      color: $light-text;
      overflow-y: auto;
      padding: 20px 0 20px 10px;
      transform: rotateY(180deg);

      img {
        vertical-align: middle;
        width: 18px;
        height: 14px;
      }

      h2 {
        margin-bottom: 20px;
      }

      p {
        margin: 10px 0;
      }

      .overview {
        margin: 0 5px 10px 0;
        line-height: 1.4em;
      }

      .divisor {
        width: 98%;
        border-top: 2px solid $light-text;
      }

      .containerGenres {
        margin-top: 10px;

        h4 {
          margin-bottom: 10px
        }

        .singleCardGenre {
          @include compileFlex(flex-start, center);
          flex-wrap: wrap;
          list-style-type: none;

          li {
            width: auto;
            margin-bottom: 5px;
            font-size: 0.9em;

            span {
              margin: 0 5px 0 2px;
            }
          }
        }
      }

      .containerActors {
        margin-top: 10px;
        
        h4 {
          margin-bottom: 10px
        }

        p {
          text-align: start;
          font-size: 0.9em;
          width: 90%;
          line-height: 1.4em;
        }
      }

    }

    .flip-card-back::-webkit-scrollbar {
      width: 10px;
    }

    .flip-card-back::-webkit-scrollbar-track {
      background: $black;
    }

    .flip-card-back::-webkit-scrollbar-thumb {
      background-color: $primary-logo;
      border-radius: 16px;
      border: 3px solid $black;
    }
  }


  @media screen and (max-width: 490px) {
    .containerCards {
      width: 270px;
    }

  }
</style>