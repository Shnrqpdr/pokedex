<template>
<div>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
    pokemonsList: [],
  }
  },
  created() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0.').then(response => {
      this.pokemonsList = response.data.results;
    });
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
