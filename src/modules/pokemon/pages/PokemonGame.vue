<!-- Seccion de HTML -->
<template>
  <section
    v-if="isLoading || randomPokemon.id === null"
    class="flex flex-col justify-center items-center w-screen h-screen"
  >
    <h1 class="text-3xl">Espere por favor</h1>
    <h3 class="animate-pulse">Cargando Pokemons</h3>
  </section>

  <section v-else class="flex flex-col justify-center items-center w-screen h-screen">
    <h1 class="m-5">¿Quién es este Pokémon?</h1>
    <h3 class="capitalize">{{ gameStatus }}</h3>
    <div class="h-20">
      <button
        v-if="gameStatus !== GameStatus.Playing"
        @click="getNextRound(4)"
        class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-700 transition-all"
      >
        ¿Jugar de nuevo?
      </button>
    </div>

    <!-- Pokemon Picture -->
    <PokemonPicture
      :pokemon-id="randomPokemon.id"
      :show-pokemon="gameStatus !== GameStatus.Playing"
    />
    <!-- Pokemon Option  -->
    <PokemonOptions
      :options="options"
      :block-selection="gameStatus !== GameStatus.Playing"
      :correct-answer="randomPokemon.id"
      @selected-option="checkAnswer"
    />

    <!-- Contadores de victorias y derrotas -->
    <div class="fixed bottom-5 left-5 bg-green-500 text-white p-2 rounded-md">
      Victorias: {{ victories }}
    </div>
    <div class="fixed bottom-5 right-5 bg-red-500 text-white p-2 rounded-md">
      Derrotas: {{ defeats }}
    </div>
  </section>
</template>

<!-- Seccion de script -->
<script setup lang="ts">
import PokemonPicture from '@/modules/pokemon/components/PokemonPicture.vue';
import PokemonOptions from '@/modules/pokemon/components/PokemonOptions.vue';
import { usePokemonGame } from '../composables/usePokemonGame';
import { GameStatus } from '../interfaces';

const {
  randomPokemon,
  isLoading,
  gameStatus,
  pokemonOptions: options,
  checkAnswer,
  getNextRound,
  victories,
  defeats,
} = usePokemonGame();
</script>
