<template>
  <header>
    <LogoComp />

    <div id="searchCont">

      <form action="" class="search">
        <!-- @keydown.enter.prevent="$emit( 'search', inputText )" : poteva essere inserito nell'input 
        (emit identico a quello del button): il "keyup" non accetta il prevent -->
        <input type="text" class="searchInput" placeholder="Cerca il tuo film preferito!" v-model.trim="inputText">

        <button type="submit" class="btnSearch" @click.prevent="$emit( 'search', inputText )">
          <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
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
    },

    data() {
      return {
        inputText: "",
      }
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  @import '../style/global.scss';

  header {
    @include compileFlex (space-between, center);

    background-color: $black;
    padding: 0 25px;
    height: 10vh;



    div#searchCont {
      @include compileFlex (space-around, center);
      flex-basis: 25%;

      form.search {
        width: 100%;
        @include compileFlex (initial, initial);

        .searchInput {
          width: 100%;
          outline: none;
          border: none;
          border-color: $primary-logo;
          padding-left: 10px;
          // border-radius: 3px;
        }

        .btnSearch {
          padding: 7px 20px;
          background-color: $primary-logo;
          outline: none;
          border: none;
          border-left: 1px solid $black;
          cursor: pointer;

          &:hover .fa-magnifying-glass {
            opacity: 0.3;
            transform: scale(1.1);
          }

          .fa-magnifying-glass {
            color: $black;

          }
        }
      }
    }
  }
</style>