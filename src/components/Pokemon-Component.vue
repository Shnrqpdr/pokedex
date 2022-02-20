<template>
  <div>
      <h1>{{indexPokedex}} {{ namePokemon }}</h1>
      <small>{{url}}</small>
  </div>
</template>

<script>
export default {
    props: {
        name: String,
        url: String,
        indexPokedex: Number,
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