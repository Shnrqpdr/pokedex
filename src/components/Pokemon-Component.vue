<template>
  <div id="pokemonCard">
      <div class="card">
        <div class="card-image">
            <figure>
            <img :src="currentImg" alt="Placeholder image">
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
                <button class="button is-fullwidth" @click="mudarSpriteImg()">Mudar Sprite</button>
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
            isFront: true,
            currentImg: '',
            conteudoPokemon: {},
        }
    },
    created() {
        axios.get(this.url).then(response => {
            this.conteudoPokemon = {
                type: response.data.types[0].type.name[0].toUpperCase() + response.data.types[0].type.name.slice(1),
                imageFront: response.data.sprites.front_default,
                imageBack: response.data.sprites.back_default,
            };
            this.currentImg = this.conteudoPokemon.imageFront;
        })
    },
    computed: {
        namePokemon(){
            return this.name[0].toUpperCase() + this.name.slice(1);
        },
    },
    methods: {
        mudarSpriteImg() {
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.conteudoPokemon.imageBack;
            }else{
                this.isFront = true;
                this.currentImg = this.conteudoPokemon.imageFront;
            }
        },
    },
}
</script>

<style>
#pokemonCard{
    margin-bottom: 24px;
}
</style>