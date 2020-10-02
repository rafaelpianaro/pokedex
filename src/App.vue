<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/images/logos/download.png" alt="" />
      <h4 class="is-size-4">Pokedex</h4>
      <input class="input is-rounded" type="text" placeholder="Buscar" v-model="busca">
      <button class="button is-fullwidth is-link is-outlined btn-busca" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <!-- <h1>{{index+1}} {{poke.name}}</h1> -->
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("Pegou lista");
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
        // console.log(this.pokemons);
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar(){
      this.filteredPokemons = this.pokemons
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons
      }else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  computed: {
    // resultadoBusca(){
    //   if(this.busca == '' || this.busca == ' '){
    //     return this.pokemons
    //   }else {
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    //   }
    // }
  }
};
</script>

<style>
.btn-busca {
  margin-top: 10px;
}
</style>

