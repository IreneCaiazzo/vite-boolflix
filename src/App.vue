<script>
import axios from 'axios';

export default {
  data() {
    return {
      inputText: "",
      arrMovies: [],
    };
  },

  methods: {
    searchAPI() {
      axios.get('https://api.themoviedb.org/3/movie/550?api_key=f51bb24ca7ecc81a5e33bda999a99446', {
        params: {
          query: this.inputText
        }
      })
        .then(response => {
          this.arrMovies = response.data;
        });
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
        <input type="text" v-model="inputText" @keyup.enter="searchAPI">
        <button @click="searchAPI">Cerca</button>
      </div>
    </nav>
  </header>

  <main>
    <div class="container">

      <ul v-for="movie in arrMovies">
        <li>{{ movie.title }}</li>
        <li>{{ movie.original_title }}</li>
        <li>{{ movie.original_language }}</li>
        <li>{{ movie.vote_average }}</li>
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
</style>
