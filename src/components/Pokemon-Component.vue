<template>
  <div>
      <h1>{{indexPokedex}} {{ namePokemon }}</h1>
      <small>{{url}}</small>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    props: {
        name: String,
        url: String,
        indexPokedex: Number,
    },
    data() {
        return {
            conteudoPokemon: {},
        }
    },
    created() {
        axios.get(this.url).then(response => {
            this.conteudoPokemon = {
                type: response.data.types[0].type.name,
                imageFront: response.data.sprites.front_default,
                imageBack: response.data.sprites.back_default,
            };
            console.log('testando: ', this.conteudoPokemon);
        })
    },
    computed: {
        namePokemon(){
            var newName = this.name[0].toUpperCase() + this.name.slice(1);
            return newName;
        }
    }
}
</script>

<style>

</style>