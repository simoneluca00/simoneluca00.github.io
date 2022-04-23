<template>
  <main>
        <FilmsComp :films="films"/>

        <SeriesComp :tvSeries="tvSeries"/>
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
  },

}
</script>

<style lang="scss">
@import '../style/global.scss';

main {
    background-color: $main-gray;
    min-height: 90vh;

    div.sectionTitle {
      display: flex;
      justify-content: center;
      font-family: sans-serif;
      color: $white;
      padding: 10px 0;

      h2 {
        text-transform: uppercase;
        text-align: center;

      }
      
      span {
        font-size: 0.9em;
        font-weight: bold;
        align-self: flex-end;
        margin-bottom: 4px;
        margin: 0 0 5px 4px;
      }
    }

    
}

</style>