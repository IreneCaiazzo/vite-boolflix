<script>
import HeaderApp from './components/HeaderApp.vue';
import CardList from './components/CardList.vue';
import Card from './components/Card.vue';
import axios from 'axios';
import { store } from './store';

export default {
  data() {
    return {
      store,
    };
  },

  components: {
    HeaderApp,
    CardList,
    Card,
  },

  created() {
    axios.get('https://api.themoviedb.org/3/search/movie').then(response => (this.store.arrMovies = response.data.data));
  },
}
</script>

<template>
  <HeaderApp />
  <CardList />
</template>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
