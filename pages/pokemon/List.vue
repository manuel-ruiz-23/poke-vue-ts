<template>
    <div>
        <ul v-if="pokemons.length > 1">
            <li v-for="pokemon in pokemons" :key="pokemon.name">
                <nuxt-link :to="`/pokemon/${pokemon.name}`">
                    {{ pokemon.name }}
                </nuxt-link>
            </li>
        </ul>
        <div id="details">
            
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { PokemonType } from '~/types';

export default Vue.extend({
    name: 'ListPage',
    data() {
        return {
            pokemons: [] as { name: string, url: string}[],
            selectedPokemon: {} as PokemonType,
        }
    },
    async asyncData({ $axios }) {
        const response = await $axios('https://pokeapi.co/api/v2/pokemon?limit=151');
        console.log('response', response.data.results);
        return { pokemons: response.data.results };
    }
})
</script>

<style scoped>
    ul {
        max-height: 90vh;
        overflow-y: scroll;
        padding: 0;
        max-width: 50%;
    }

    li {
        list-style: none;
        margin-bottom: 8px;
        border: 1px solid #ccc;
        height: 32px;
        padding-left: 16px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>