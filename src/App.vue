<template>
  <div id="app">
    <!-- Panel central -->
    <img class="img-banner" alt="Vue logo" src="./assets/logo.png" />
    <h2 class="my-4">PokeGuía</h2>
    <label class="mr-2">Nombre:</label>
    <input type="text" placeholder="Ingrese un pokémon" v-model="pokemonName" />
    <button @click="searchPokemon()">Buscar</button>
    <!-- Imagen de Pokemon buscado -->
    <div>
      <img :src="pokemon.sprites.front_default" />
    </div>
    <div>
      <h2>Movimientos</h2>
      <p v-for="(movimiento, $index) in moves" :key="$index">
        {{ movimiento.move.name }}
      </p>
    </div>
    <div>
      <h2>Habilidades</h2>
      <p v-for="(habilidad, $index) in abilities" :key="$index">
        {{ habilidad.ability.name }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    pokemonName: 'pikachu',
    pokemon: null
  }),
  methods: {
    searchPokemon() {
      console.log(this.pokemonName)
      this.fetchPokemon()
    },
    fetchPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemonName}`)
        .then((response) => response.json())
        .then((json) => (this.pokemon = json))
    }
  },
  computed: {
    moves() {
      return this.pokemon.moves
    },
    abilities() {
      return this.pokemon.abilities
    }
  },

  created() {
    this.searchPokemon()
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>