<template>
    <div  class="flex justify-center">
        <img v-if="!showPokemon" class="hidden-pokemon w-96 h-96":src="img" alt="imagen-pokemon" />
        <img v-else :src="img" alt="imagen-pokemon" class="w-96 h-96"/>
    </div>
</template>

<script lang="ts" setup>
    const props = defineProps<{
        pokemonId: number,
        showPokemon: boolean
    }>()

    const img = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${ props.pokemonId }.svg`;


</script>

<style>
    .hidden-pokemon{
        filter: brightness(0);
    }

</style>