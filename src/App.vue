<template>
  <div class="row">
    <h1>Seja bem-vindo à Pokedex</h1>
    <p>Por favor, digite abaixo o número do pokemon desejado</p>
    <input type="number" v-model="search" />
    <button style="margin-left: 20px;" @click="atualizaPokemon">Procurar</button>
  </div>
  <div class="row" v-if="catched">
    <h1 class="namePokemon">{{ pokemons.name }}</h1>
    <img :src="pokemons.sprites.front_default" :alt="pokemons.name" />
  </div>
</template>

<script lang="ts">
import axios from "axios"

export default {
  name: "Pokedex",
  data: () => {
    return {
      pokemons: [],
      PokeData: [],
      search: "",
      catched: false,
    }
  },
  mounted() {
    axios.get("https://pokeapi.co/api/v2/pokemon").then((response) => {
      this.PokeData = response.data.results
    })
    console.log("Catched'em All!")
  },

  methods: {
    atualizaPokemon() {
      axios.get("https://pokeapi.co/api/v2/pokemon/" + this.search).then((response) => {
        console.log(response);
        this.pokemons = response.data
      })
      this.catched = true
    },
  },

}
</script>

<style>
input,
button {
  flex: 1;
  border-width: 1;
  border-color: #ccc;
  margin: 0 10;
  border-radius: 20%;
  padding: 10px;
  font-size: 18px;
}

img {
  width: 200px;
  height: 200px;
}

.namePokemon {
  font-size: 30px;
  font-weight: bold;
  text-align: center;
  text-transform: capitalize;
}
</style>
