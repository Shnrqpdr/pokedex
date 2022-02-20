<template>
  <div id="pokemonCard">
      <div class="card">
        <div class="card-image">
            <figure>
            <img :src="conteudoPokemon.imageFront" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{indexPokedex}} - {{ namePokemon }}</p>
                    <p class="subtitle is-6">{{ conteudoPokemon.type }}</p>
                </div>
            </div>

            <div class="content">
            </div>
        </div>
    </div>
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
#pokemonCard{
    margin-bottom: 24px;
}
</style>