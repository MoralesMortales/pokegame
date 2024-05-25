<template>
    <div class="grid grid-cols-2 gap-12 items-center mx-32 mt-6 space-y-1"> 

        <button
        @click="$emit('selectionPokemon' ,pokemon.id)" 
        class="text-3xl border-4 p-2 rounded-2xl text-center" 
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        :disabled="showPokemon == true || showAnswers == true">
            {{ pokemon.name }}   
    </button>
    </div>  
   
</template>

<script lang="ts" setup>

import type { Pokemon } from 'env'

defineProps<{
    pokemon1: Pokemon|undefined,
    pokemons: Pokemon[],
    showPokemon: boolean,
    showAnswers: boolean
    }>()    

</script>