<template>
  <div id="app">
    <div v-for="(poke, index) in pokemons" :key="index">
      <!-- <h1>{{index+1}} {{poke.name}}</h1> -->
      <Pokemon :name='poke.name' :url='poke.url' :num='index+1' />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data(){
    return {
      pokemons: []
    }
  },
  created() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      console.log('Pegou lista')
      this.pokemons = res.data.results
      console.log(this.pokemons)
    })
  },
  components: {
    Pokemon
  }
}
</script>

<style>

</style>
