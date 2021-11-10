<template>
<div class="container">
  <div class="card">
    <h2 class="pokemon-name">#{{ id }} - {{ name }}</h2>
    <img :src="this.img_pokemon" class="pokemon-img" alt="">
    <button v-on:click="changePositionImg">Cambiar posición</button>
  </div>
</div>
</template>

<script>

export default {
name: "PokemonDetails",
  data() {
  return {
    img_pokemon: '',
    img_front: '',
    img_back: ''
  }
  },
  props: {
    id: Number,
    name: String,
    url: String
  },
  methods: {
    getPokemonImg() {
      this.axios.get(this.url)
      .then(response => {
        this.img_front = response.data.sprites.front_default
        this.img_back = response.data.sprites.back_default
        this.img_pokemon = this.img_front
        console.log(response.data.sprites.front_default)
      })
      .catch(error => {
        console.log(error)
      })
    },
    changePositionImg() {
      if(this.img_pokemon !== this.img_front) {
        this.img_pokemon = this.img_front
      }
      else {
        this.img_pokemon = this.img_back
      }
    }
  },
  created() {
    this.getPokemonImg()
  }
}
</script>

<style>
.container {
  margin-top: 35px;
}

.pokemon-img {
  width: 150px;
  height: 150px;
}
.card {
  background: black;
  box-shadow: 0 0 20px rgba(0,0,0,0.4);
  border-radius: 5px;
  margin: 80px 50px 50px 50px;
  width: 250px;
  padding: 20px;
  text-align: center;
  color: white;
  float: left;
  height: 250px;
}
</style>