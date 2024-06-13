<script setup>
import { onMounted, ref, computed } from "vue"
import axios from "axios"
import Pokemon from "./components/Pokemon.vue"

const pokemones = ref([])
const count = ref(0)
const computedPokemons = computed(() => pokemones.value)

const getPokemons = async () => {
  try {
    const { data } = await axios('https://pokeapi.co/api/v2/pokemon')
    pokemones.value = data.results
  } catch (error) {
    console.log(error.message);
  }
}

onMounted(getPokemons)
</script>

<template>
  <div class="adivinapokemon">
    <div class="adivinapokemon__logo">
      <img src="/pokemontitle.svg" class="logo" alt="pokemon logo" />
    </div>

    <h1 class="adivinapokemon__titulo">
      ¿Quién es ese Pokémon?
    </h1>

    <p class="adivinapokemon__cantidad">
      Pokemones descubiertos: <span>{{ count }}</span>
    </p>

    <div class="adivinapokemon__grid">
      <Pokemon v-for="pokemon in computedPokemons" :pokemon="pokemon" :key="pokemon.name"
        @descubrirPokemon="i => count += i" />
    </div>
  </div>
</template>

<style scoped>
.adivinapokemon__logo {
  width: 15rem;
  margin: 0 auto;
}

.adivinapokemon__cantidad {
  font-weight: 900;
}

.adivinapokemon__cantidad span {
  color: palegoldenrod;
}

.adivinapokemon__grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
}
</style>
