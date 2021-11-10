<template>
  <div id="app">
    <h1 class="title">LISTADO DE POKEMONES CON VUE.js</h1>
    <div v-for="(pokemon, index) in pokemon_arr" v-bind:key="index">
      <PokemonDetails :id="index +1" :name="pokemon.name" :url="pokemon.url" />

    </div>

  </div>
</template>

<script>
import PokemonDetails from './components/PokemonDetails.vue'


export default {
  name: 'App',
  components: {
    PokemonDetails
  },
  data() {
    return {
      pokemon_arr: []
    }
  },
  methods: {
    getPokemonData() {
      this.axios.get('https://pokeapi.co/api/v2/pokemon?limit=51')
      .then(response => {
        this.pokemon_arr = response.data.results;
        console.log(response.data.results)
      })
      .catch(error => {
        console.error(error)
      })
    }
  },
  mounted() {
    this.getPokemonData()
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Varela+Round&display=swap');

body {
  background-color: #6b6969;
  font-family: 'Varela Round', sans-serif;
  color: aliceblue;
}
.title {
  text-align: center;
}
</style>
