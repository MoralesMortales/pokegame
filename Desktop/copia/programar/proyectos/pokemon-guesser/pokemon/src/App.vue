<script setup lang="ts">
  import type { Pokemon } from 'env';
  import getPokemonOptions from './api/getPokemonOptions';
  import { ref } from 'vue';
  import PokemonOptions from './components/PokemonOptions.vue';
  import PokemonPicture from './components/PokemonPicture.vue';
  

  const pokemonArr = ref<any>([])
  const pokemon = ref<Pokemon>()

  const mixPokemonArray = async()=>{
    pokemonArr.value = await getPokemonOptions()
    const randomInt = Math.floor(Math.random() * 4)
    pokemon.value = pokemonArr.value[randomInt]
    
  }

  mixPokemonArray()
</script>

<template>
  <div class="m-12">
    <PokemonPicture v-if="pokemon" :pokemon-id="pokemon.id" />
    <PokemonOptions :pokemons="pokemonArr" /> 
  </div>

  <!-- <div class="flex justify-center mt-14" v-for=""pokemon in pokemons
  <p class="text-9xl">hola tonotos</p> -->

</template>

