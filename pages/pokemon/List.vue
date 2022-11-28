<template>
    <div id="poke-list-page">
        <nuxt-link to="/">Inicio</nuxt-link>
        <ul v-if="pokemons.length > 1">
            <li
                v-for="pokemon in pokemons"
                :key="pokemon.name"
                @click="selectedPokemonName = pokemon.name"
                :class="selectedPokemonName === pokemon.name ? 'selected' : ''"
            >
                <p>
                    {{ pokemon.name }}
                </p>
            </li>
        </ul>
        <div id="details">
            <PokeDetails v-if="selectedPokemon?.name" :pokemon="selectedPokemon" />
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { PokemonType } from '~/types';

export default Vue.extend({
    name: 'ListPage',
    async asyncData({ $axios }) {
        const response = await $axios('https://pokeapi.co/api/v2/pokemon?limit=151');
        return { pokemons: response.data.results };
    },
    data() {
        return {
            pokemons: [] as { name: string, url: string }[],
            selectedPokemonName: "",
            selectedPokemon: {} as PokemonType,
        }
    },
    watch: {
        selectedPokemonName: async function () {
            const response = await this.$axios(`https://pokeapi.co/api/v2/pokemon/${this.selectedPokemonName}`);
            this.selectedPokemon = response.data;
            console.log('selectedPokemon', this.selectedPokemon);
        }
    }
})
</script>

<style scoped>
#poke-list-page {
    display: flex;
    gap: 32px;
}

#details {
    flex: 1;
}

ul {
    max-height: 90vh;
    overflow-y: scroll;
    padding: 0;
    max-width: 50%;
    flex: 1;
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
    cursor: pointer;
}

li.selected {
    background-color: #ccc;
}
</style>