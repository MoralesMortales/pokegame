<template>
    <div class="grid grid-cols-2 gap-5 items-center justify-items-center"> 
        <button @click="$emit('selectionPokemon' ,pokemon.id)" 
        class="text-3xl border-4 p-2 rounded-2xl text-center w-2/3 hover:bg-slate-300 hover:cursor-pointer" 
        v-for="pokemon in pokemons" :key="pokemon.id" :disabled = "showPokemon == true || showAnswers == true" >
        
            {{ pokemon.name }}   
    </button>
</div>   
    
</template>

<script lang="ts" setup>

    import type { Pokemon } from 'env'

    defineProps<{
        pokemon1: Pokemon|undefined,
        pokemons: Pokemon[],
        showPokemon:boolean,
        showAnswers:boolean
    }>()    

</script>