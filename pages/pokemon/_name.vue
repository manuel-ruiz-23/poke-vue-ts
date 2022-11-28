<template>
  <div>
    <nuxt-link to="/">Inicio</nuxt-link>
    <PokeDetails :pokemon="pokemon" />
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

<style scoped>
#poke-details {
  display: flex;
  flex-wrap: wrap;
  gap: 32px;
  justify-content: center;
  align-items: center;
}
</style>