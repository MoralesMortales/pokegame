<script setup lang="ts">
import type { Pokemon } from 'env';
  import getPokemonOptions from './api/getPokemonOptions';
  import { ref } from 'vue';
  

  const pokemonArr = ref<any>([])
  const pokemon = ref<Pokemon>()

  const mixPokemonArray = async()=>{
    pokemonArr.value = await getPokemonOptions()
    const randomInt = Math.floor(Math.random() * 4)
    pokemon.value = pokemonArr.value[randomInt]
    console.log(pokemon.value)
    console.log(pokemonArr.value)
  }

  mixPokemonArray()
</script>

<template>
 <p class="text-9xl">hola tonotos</p>
</template>

