<script>
import axios from 'axios';
import LangFlag from 'vue-lang-code-flags/LangFlag.vue';

export default {
  data() {
    return {
      inputText: "",
      arrMovies: [],
      arrSeries: [],
    };
  },

  components: {
    LangFlag,
  },

  methods: {

    searchAPI(url, objParams, varResult) {
      axios
        .get(url, {
          params: objParams,
        })
        .then(response => {
          if (response.request.responseURL.includes('/search/movie')) {

            this.arrMovies = response.data.results;
          } else {
            this.arrSeries = response.data.results;
          }

        });
    },

    requestToApi(inputText) {

      const objParams = {
        api_key: 'f51bb24ca7ecc81a5e33bda999a99446',
        query: this.inputText
      };


      this.searchAPI('https://api.themoviedb.org/3/search/movie',
        objParams,
        this.arrMovies
      ); //film

      this.searchAPI('https://api.themoviedb.org/3/search/tv',
        objParams,
        this.arrSeries
      ); //serie
    }
  },

  created() {
    axios.get('https://api.themoviedb.org/3/search/movie?api_key=f51bb24ca7ecc81a5e33bda999a99446&query=avengers')
      .then((response) => this.arrMovies = response.data.results);
  },
}
</script>

<template>
  <header>
    <nav>
      <h1>Boolflix</h1>
      <div class="search">
        <input type="text" v-model="inputText" @keyup.enter="requestToApi">
        <button @click="requestToApi">Cerca</button>
      </div>
    </nav>
  </header>

  <main>
    <div class="container">
      <ul>
        <li v-for="movie in arrMovies" :key="movie.id">
          {{ movie.title }}
          {{ movie.original_title }}
          <LangFlag :iso="movie.original_language" :squared="false" />
          <span class="lang-text">{{ movie.original_language }}</span>
          {{ movie.vote_average }}
        </li>
      </ul>

      <ul>
        <li v-for="serie in arrSeries" :key="serie.id">

        </li>
      </ul>
    </div>
  </main>
</template>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 5rem;
  background-color: black;
  color: red;
  padding-inline: 2rem;

  input {
    margin-right: 1rem;
  }
}

.lang-text {
  display: none;
}

.flag-icon-undefined {
  display: none;
}

.flag-icon-undefined+.lang-text {
  display: inline;
}
</style>
