<template>
  <div>
    <!-- <small>{{ url }}</small> -->
    <div class="buttons">
        <button class="button is-primary">Primary</button>
        </div>
    <div class="card">
      <div class="card-content">
        <div class="media">
            <div class="media-left">
                <figure class="image is-96x96">
                <img :src="pokemon.front" :alt="pokemon.url" />
                </figure>
            </div>
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ name | upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>
        <div class="content">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created() {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
    //   console.log(this.pokemon)
    });
  },
  data() {
    return {
      pokemon: {
          type: '',
          front: '',
          back: ''
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper(value) {
      let newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
};
</script>

<style>
</style>