<script setup lang="ts">
  import type { Pokemon } from 'env';
  import getPokemonOptions from './api/getPokemonOptions';
  import { ref } from 'vue';
  import PokemonOptions from './components/PokemonOptions.vue';
  import PokemonPicture from './components/PokemonPicture.vue';

  const pokemonArr = ref<any>([]);
  const pokemon = ref<Pokemon>();
  const showPokemon = ref<boolean>(false);
  const showAnswers = ref<boolean>(false);
  const message = ref<string>();
  const streack = ref<number>(0);

  const mixPokemonArray = async () => {
    pokemonArr.value = await getPokemonOptions();
    const randomInt = Math.floor(Math.random() * 4);
    pokemon.value = pokemonArr.value[randomInt];
  };

  const checkAnswer = (selectedId: number) => {
    showPokemon.value = true;
    showAnswers.value = true;

    if (selectedId === pokemon.value?.id) {
      streack.value++;
      message.value = `Well done, it was a ${pokemon.value.name}`;
    } else {
      streack.value = 0;
      const motivationalMessage = [
        `That is not right, the answer is a ${pokemon.value?.name}`,
        `Wrong answer, the right one is a ${pokemon.value?.name}`,
        `Try again, it is a ${pokemon.value?.name}`,
        `No... It is a ${pokemon.value?.name}`,
        `Almost there, it was a ${pokemon.value?.name}`,
        `Another shot? It was a ${pokemon.value?.name}`,
        `Wrong, try again, it was a ${pokemon.value?.name}`,
        `Quite based, but no, it is a ${pokemon.value?.name}`,
      ];
      const randomInt = Math.floor(Math.random() * motivationalMessage.length);
      message.value = motivationalMessage[randomInt];
    }
  };

  const newGame = () => {
    showPokemon.value = false;
    showAnswers.value = false;
    pokemonArr.value = [];
    pokemon.value = undefined;

    mixPokemonArray();
  };

  mixPokemonArray();
</script>

<template>
  <div class="p-5 bg-gray-400  h-screen justify-around gap-2 flex flex-col">

    <div class=" h-1/6 ">
      <PokemonPicture :show-pokemon="showPokemon" v-if="pokemon" :pokemon-id="pokemon.id" class="" />
    </div>

    <div class="flex justify-center text-4xl font-bold h-1/6 py-2 items-center">
      {{ streack }}
    </div>

    <div class="h-3/6 justify-around flex flex-col w-full">
      <PokemonOptions
        :pokemon1="pokemon"
        :show-pokemon="showPokemon"
        :show-answers="showAnswers"
        @selection-pokemon="checkAnswer"
        :pokemons="pokemonArr"
      />
    </div>

    <div v-if="showAnswers" class="flex flex-col text-center h-2/6 items-center justify-around">
      <p class=""> {{ message }}</p>
      <button @click="newGame" class="font-bold">New Game</button>
    </div>
</div>
</template>
