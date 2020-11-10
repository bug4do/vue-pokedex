a<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h1 class="title is-3">Pokedex</h1>
      <input type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-rounded">
      <hr>
      <div v-for="(poke, index) in buscaResult" :key="index" class="list">
          <Pokemon :id="index" :name="poke.name" :url="poke.url"/>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  components: {
    Pokemon
  },
  data() {
    return {
      busca: '',
      pokemons: []
    }
  },
  computed: {
    buscaResult: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
sd2        console.log(this.pokemons);
        return this.pokemons.filter(pokemon => pokemon.name.toLowerCase() == this.busca.toLowerCase());
      }
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=251&offset=0').then(res => {
      this.pokemons = res.data.results;
    });
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
