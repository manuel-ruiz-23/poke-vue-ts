<template>
<div>
    <input @keyup.enter="searchPokemon" type="text" v-model="search" />
    <button @click="searchPokemon">Buscar</button>

    <div v-if="loading">
      <p>Buscando...</p>
    </div>

    <div v-if="pokemon">
      <p>{{ pokemon.name }}</p>
      <img :src="pokemon.sprites.front_default" />
    </div>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import { PokemonType } from '~/types';

export default Vue.extend({
  name: 'Search',
  data() {
    return {
      search: '',
      loading: false,
      pokemon: undefined as PokemonType | undefined,
    }
  },
  methods: {
    async searchPokemon() {
      this.loading = true
      const response = await this.$axios.$get(`https://pokeapi.co/api/v2/pokemon/${this.search}`)
      console.log(response);
      this.pokemon = response;
      this.loading = false
    },
  },
})

</script>