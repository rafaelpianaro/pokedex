<template>
  <div id="app">
    <div class="buttons">
      <button class="button is-primary">clique aqui</button>
      
    </div>
  </div>
</template>

<script>
import axios from 'axios'

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
    
  }
}
</script>

<style>

</style>
