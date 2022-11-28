<template>
<div id="search">
    <input placeholder="Pokemon search" @keyup.enter="searchPokemon" type="text" v-model="search" />
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

<style scoped>
  #search {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  input {
    width: 256px;
    height: 24px;
    border: none;
    border-radius: 8px;
    text-align: center;
    margin-bottom: 8px;
  }

  button {
    height: 32px;
    min-width: 64px;
    width: min-content;
    background-color: #00DC81;
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
  }
</style>