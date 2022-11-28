<template>
<div id="search">
    <input placeholder="Pokemon search" @keyup.enter="searchPokemon" type="text" v-model="search" />
    <ButtonCommon @click="searchPokemon">Buscar</ButtonCommon>
    <br />

    <div v-if="loading">
      <p>Buscando...</p>
    </div>

    <div v-if="pokemon">
      <p>{{ pokemon.name }}</p>
      <img :src="pokemon.sprites.front_default" />
      <nuxt-link :to="`/pokemon/${pokemon.name}`">Ver detalles</nuxt-link>
    </div>
    

    <ButtonCommon to="/pokemon/list">Ver Lista</ButtonCommon>
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
      console.log('searching pokemon');
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
</style>