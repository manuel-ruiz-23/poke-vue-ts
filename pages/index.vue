<template>
  <div>
    <h1>Poke-Vue-Ts</h1>
    <Search />

    <nuxt-link to="/pokemon/pikachu">Pikachu</nuxt-link>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'IndexPage',
})
</script>

<style scoped>
  h1 {
    color: #00693E;
    text-align: center;
  }
</style>
