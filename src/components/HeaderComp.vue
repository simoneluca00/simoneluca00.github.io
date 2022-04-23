<template>
  <header>
    <LogoComp />

    <div id="search">
      <form action="">
        <input type="text" class="searchInput" placeholder="Cerca il tuo film preferito" v-model.trim="inputText">

        <button type="submit" class="btnSearch" @click.prevent="$emit( 'performSearch', inputText )">
          Cerca
        </button>
      </form>
    </div>

  </header>
</template>

<script>
  import LogoComp from './partials/LogoComp.vue'

  export default {
    name: 'HeaderComp',

    components: {
      LogoComp,
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../style/global.scss';

  header {
    @include compileFlex (space-between, center);

    background-color: #000;
    padding: 10px 25px;

    div#search {
      flex-basis: 25%;

      form {
        width: 100%;
        @include compileFlex (initial, initial);

        .searchInput {
          width: 80%;
          outline: none;
          border: none;
          padding-left: 10px;
          border-radius: 3px;
        }

        .btnSearch {
          padding: 8px 20px;
          color: $white;
          letter-spacing: 0.03em;
          background-color: $primary-red;
          outline: none;
          border: none;
        }
      }
    }
  }
</style>