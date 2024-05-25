<script setup lang="ts">
  import type { Pokemon } from 'env';
  import getPokemonOptions from './api/getPokemonOptions';
  import { ref } from 'vue';
  import PokemonOptions from './components/PokemonOptions.vue';
  import PokemonPicture from './components/PokemonPicture.vue';
  
  const pokemonArr = ref<any>([])
  const pokemon = ref<Pokemon>()
  const showPokemon = ref<boolean>(false)
  const showAnswers = ref<boolean>(false)
  const message = ref<string>()
  const streack = ref<number>(0)

  const mixPokemonArray = async()=>{
    pokemonArr.value = await getPokemonOptions()
    const randomInt = Math.floor(Math.random() * 4)
    pokemon.value = pokemonArr.value[randomInt]
    
  }

  const checkAnswer = (selectedId: number)=>{

    showPokemon.value = true
    showAnswers.value = true

    if(selectedId === pokemon.value?.id){
      streack.value++
      message.value = `Correcto, era un ${pokemon.value.name}`
    }
    else{
      streack.value = 0
      const motivationalMessage = [
        `Mira huele pega, eso es un ${pokemon.value?.name}`,
        `Marico debe ser que te lanzaron contra el suelo de pequeño, eso es un ${pokemon.value?.name}`,
        `Mamabicho te encanta que te maltraten?, eso es un ${pokemon.value?.name}`,
        `Eres marico o te amamantaban con pegamento?, eso es un ${pokemon.value?.name}`,
        `Eres jugador de fate? porque te faltan neuronas, eso es un ${pokemon.value?.name}`,
        `Desgracia familiar, eso es un ${pokemon.value?.name}`,
        `Fenomeno de 3 cromosomas, eso es un ${pokemon.value?.name}`,
        `te falta escencia, eso es un ${pokemon.value?.name}`
      ]
      const randomInt = Math.floor(Math.random() * motivationalMessage.length)
      message.value = motivationalMessage[randomInt]
    }
  }
  
  const newGame =()=>{
    showPokemon.value = false
    showAnswers.value = false
    pokemonArr.value = []
    pokemon.value = undefined

    mixPokemonArray()
  }

  mixPokemonArray()
</script>

<template>
  <div class="bg-gray-600 h-screen p-5 flex flex-col justify-around" id="container">

    <div class=" h-2/6">
    
      <PokemonPicture :show-pokemon="showPokemon" v-if="pokemon" :pokemon-id="pokemon.id" class=""/>  
  
    </div>

    <div class="flex justify-center text-4xl font-bold h-1/6 items-center">
      {{ streack }}
    </div>

    <div class="">
      
      <PokemonOptions 
      :pokemon1="pokemon"
      :show-pokemon="showPokemon" 
      :show-answers="showAnswers" 
      @selection-pokemon="checkAnswer" 
      :pokemons="pokemonArr"/>

    </div>
    
    <div v-if="showAnswers" class="flex flex-col text-center gap-3 h-1/6 items-center justify-center"> 
      
      <p class=""> {{ message }}</p>
    
      <button @click="newGame" class="font-bold">New Game</button>
    </div>   
    
  </div>


</template>


<script setup lang="ts">
  import type { Pokemon } from 'env';
  import getPokemonOptions from './api/getPokemonOptions';
  import { ref } from 'vue';
  import PokemonOptions from './components/PokemonOptions.vue';
  import PokemonPicture from './components/PokemonPicture.vue';
  

  const pokemonArr = ref<any>([])
  const pokemon = ref<Pokemon>()
  const showPokemon = ref<boolean>(false)
  const showAnswers = ref<boolean>(false)
  const message = ref<string>()
  const streack = ref<number>(0)

  const mixPokemonArray = async()=>{
    pokemonArr.value = await getPokemonOptions()
    const randomInt = Math.floor(Math.random() * 4)
    pokemon.value = pokemonArr.value[randomInt]
    
  }

  const checkAnswer = (selectedId: number)=>{
    showPokemon.value = true
    showAnswers.value = true

    if(selectedId === pokemon.value?.id){
      streack.value++
      message.value = `Correcto, era un ${pokemon.value.name}`
    }
    else{
      streack.value = 0
      const motivationalMessage = [
        `Mira huele pega, eso es un ${pokemon.value?.name}`,
        `Marico debe ser que te lanzaron contra el suelo de pequeño, eso es un ${pokemon.value?.name}`,
        `Mamabicho te encanta que te maltraten?, eso es un ${pokemon.value?.name}`,
        `Eres marico o te amamantaban con pegamento?, eso es un ${pokemon.value?.name}`,
        `Eres jugador de fate? porque te faltan neuronas, eso es un ${pokemon.value?.name}`,
        `Desgracia familiar, eso es un ${pokemon.value?.name}`,
        `Fenomeno de 3 cromosomas, eso es un ${pokemon.value?.name}`,
        `te falta escencia, eso es un ${pokemon.value?.name}`
      ]
      const randomInt = Math.floor(Math.random() * motivationalMessage.length)
      message.value = motivationalMessage[randomInt]
    }
  }

  const newGame =()=>{
    showPokemon.value = false
    showAnswers.value = false
    pokemonArr.value = []
    pokemon.value = undefined

    mixPokemonArray()
  }


  mixPokemonArray()
</script>

<template>
  <div class="m-12">
    <PokemonPicture :show-pokemon="showPokemon" v-if="pokemon" :pokemon-id="pokemon.id" />
    <div class="flex justify-center text-4xl font-bold mt-12">
      <p> {{ streack }}</p>
      <p v-if="streack == 10">Estas en racha de 10 puntos</p>
    </div>

    <PokemonOptions
    
    :pokemon1="pokemon" 
    :show-pokemon="showPokemon" 
    :show-answer="showAnswers"
    @selection-pokemon="checkAnswer" 
    :pokemons="pokemonArr" /> 
  </div>

  <div v-if="showAnswers" class="flex flex-col text-center">
    <p class="text-3xl font-bold"> {{ message }}</p>
    <div>
      <button @click="newGame" class="font-bold">New Game</button>
    </div>   
  </div>

</template>

