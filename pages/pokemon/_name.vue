<template>
  <div>
    <h1>Pokemon: {{ pokemon.name }}</h1>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { PokemonType } from '~/types';

export default Vue.extend({
  name: 'PokemonPage',
  data() {
    return {
      pokemon: {} as PokemonType,
    }
  },
  async asyncData({ params, $axios }) {
    const pokemon = await $axios(`https://pokeapi.co/api/v2/pokemon/${params.name}`);
    return {
      pokemon: pokemon.data,
    }
  }
})

</script>