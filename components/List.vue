<template>
    <div>
        <ul>
            <li v-for="pokemon in pokemons" :key="pokemon.name">
                <nuxt-link :to="`/pokemon/${pokemon.name}`">
                    {{ pokemon.name }}
                </nuxt-link>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { PokemonType } from '~/types';


export default Vue.extend({
    name: 'List',
    data() {
        return {
            pokemons: [] as PokemonType[]
        }
    },
    async mounted() {
        const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
        const data = await response.json();
        this.pokemons = data.results;
    }
})

</script>