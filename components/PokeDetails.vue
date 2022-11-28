<template>
  <div id="poke-details">
    <div>
      <h1>{{ pokemon.name.toUpperCase() }}</h1>
      <img :src="pokemon.sprites.front_default" alt="front_default" />
    </div>
    <div>
      <h2>Abilities</h2>
      <ul>
        <li v-for="ability in pokemon.abilities" :key="ability.ability.name">
          {{ ability.ability.name }}
        </li>
      </ul>
    </div>
    <div>
      <h2>Types</h2>
      <ul>
        <li v-for="type in pokemon.types" :key="type.type.name">
          {{ type.type.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { PokemonType } from '~/types';

export default Vue.extend({
  name: 'PokeDetails',
  props: {
    pokemon: {
        type: Object as () => PokemonType,
        required: true,
    },
  },
})

</script>
