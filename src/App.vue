<template>
  <div id="app">
    <HeaderComp @search="searchingElement" />
    <MainComp :films="films" :tvSeries="tvSeries" :filmGenres="filmGenres" :tvSeriesGenres="tvSeriesGenres"
      :foundResults="foundResults" />
  </div>
</template>

<script>
  import axios from 'axios';

  import HeaderComp from './components/HeaderComp.vue'
  import MainComp from './components/MainComp.vue'

  export default {
    name: 'App',
    components: {
      HeaderComp,
      MainComp
    },

    data() {
      return {
        foundResults: false,
        apiKey: "8298d794dad7d9a6a86bab321846d44b",
        searchText: "",
        films: [],
        tvSeries: [],
        filmGenres: [],
        tvSeriesGenres: [],


      }
    },

    computed: {
      
    },

    methods: {
      searchingElement(text) {
        this.searchText = text;
        this.searchText = this.searchText.replace(/\s/g, '+');

        // 2) axios.all contiene i metodi che effettuano le chiamate all'API
        axios.all([
            this.filmsRequest(),
            this.tvSeriesRequest(),
            this.filmGenresRequest(),
            this.tvSeriesGenresRequest(),
          ])
          // 3) axios.spread viene utilizzato per prevenire gli errori quando si effettuano chiamate multiple all'API --> vengono passati dei parametri utilizzati al posto di "res"(chiamata singola)
          .then(axios.spread((filmsArray, tvSeriesArray, filmGenre, tvSeriesGenre) => {
            this.films = filmsArray.data.results;

            this.tvSeries = tvSeriesArray.data.results;

            this.filmGenres = filmGenre.data.genres;

            this.tvSeriesGenres = tvSeriesGenre.data.genres;
          }))
          .catch(err => console.error('Impossibile caricare i dati', err))
          .finally(() => (this.foundResults = true))

      },

      // 1) Metodo chiamata API per films
      filmsRequest() {
        return axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apiKey}&query=${this.searchText}`)
      },

      // 1) Metodo chiamata API per tvSeries
      tvSeriesRequest() {
        return axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.apiKey}&query=${this.searchText}`)
      },

      // 1) Metodo chiamata API per filmGenres
      filmGenresRequest() {
        return axios.get(`https://api.themoviedb.org/3/genre/movie/list?api_key=${this.apiKey}`)
      },

      // 1) Metodo chiamata API per tvSeriesGenres
      tvSeriesGenresRequest() {
        return axios.get(`https://api.themoviedb.org/3/genre/tv/list?api_key=${this.apiKey}`)
      },

    },

  }
</script>

<style lang="scss">
  @import './style/global.scss';

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body::-webkit-scrollbar {
    width: 12px;
  }

  body::-webkit-scrollbar-track {
    background: $black;
  }

  body::-webkit-scrollbar-thumb {
    // background-color: $primary-red;
    background-image:
      linear-gradient(to bottom,
        $black 0px,
        $black 9.9vh,
        $primary-logo 9.9vh,
        $primary-logo 100%);
    // border-radius: 20px;
    border: 3px solid $black;
  }
</style>