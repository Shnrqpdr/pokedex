<template>
<div id="app">
  <div class="column is-half is-offset-one-quarter">
    <input class="input is-rounded" type="text" placeholder="Buscar pokemon" v-model="busca" id="busca-input">
    <div v-for="(pokemon, index) in pokemonsFilteredList" :key="`pokemon-${index}`">
      <Pokemon :name="pokemon.name" :url="pokemon.url" :indexPokedex="pokemon.index"/>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon-Component';

export default {
  name: 'App',
  data() {
    return {
      pokemonsList: [],
      busca: '',
    }
  },
  components: {
    Pokemon,
  },
  async created() {
    
    await axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0.').then(response => {
      this.pokemonsList = response.data.results;
    });

    let varIndex = 0;
    this.pokemonsList.forEach(pokemon => {
      varIndex = varIndex + 1;
      pokemon.index = varIndex;
    });

  },
  computed: {
    pokemonsFilteredList() {
      if(this.busca === ''){
        return this.pokemonsList;
      }

      return this.pokemonsList.filter(p => p.name === this.busca.toLowerCase());
    },
  },
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
#busca-input {
  margin-top: 12px;
  margin-bottom: 12px;
}
</style>
