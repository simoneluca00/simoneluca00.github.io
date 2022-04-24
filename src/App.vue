<template>
  <div id="app">
    <HeaderComp @search="searchingElement"/>
    <MainComp :films="films" :tvSeries="tvSeries" :foundResults="foundResults"/>
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
      tvSeries : [],

    }
  },

  methods: {
    searchingElement(text){
      this.searchText = text;
      this.searchText = this.searchText.replace(/\s/g, '+');
      
      
      // chiamata API per films
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apiKey}&query=${this.searchText}`)
      .then((res)=> {
        this.films = res.data.results;
        console.log(this.films)   
      })
      .catch(err => console.error('Impossibile caricare i dati', err))
      .finally(() => (this.foundResults = true))

      // chiamata API per serieTV
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.apiKey}&query=${this.searchText}`)
      .then((res)=> {
        this.tvSeries = res.data.results;
        console.log(this.tvSeries)   
      })
      .catch(err => console.error('Impossibile caricare i dati', err))
      .finally(() => (this.foundResults = true))
    
    }


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
            $primary-red 9.9vh,
            $primary-red 100%);
  // border-radius: 20px;
  border: 3px solid $black;
}
</style>
