<script>
import axios from 'axios';

export default {
  data() {
    return {
      movies: [],
    };
  },

  created() {
    axios.get('https://api.themoviedb.org/3/search/movie?api_key=f51bb24ca7ecc81a5e33bda999a99446&query=avengers')
      .then((response) => this.movies = response.data.results);
  },
}
</script>

<template>
  <header>
    <nav>
      <h1>Boolflix</h1>
      <div class="search">
        <input type="text">
        <button>Cerca</button>
      </div>
    </nav>
  </header>

  <main>
    <div class="container">

      <ul>
        <li v-for="movie in movies">

          {{ movie.title }},
          {{ movie.original_title }},
          {{ movie.original_language }},
          {{ movie.vote_average }},

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
</style>
