<template>
  <div id="app">
    <input type="text" id="searchPkn" placeholder="Buscar pokemon" v-model="search"> <br>
    <button class="btnSearch" @click="buscar">Buscar</button>
    <div id="column">
      <div v-for="(poke, index) in filteredPokemon" :key="poke.url" class="column is-one-quarter" id="pokemon">
        <Poke :name="poke.name" :url="poke.url" :num="index + 1"/>
      </div>
    </div>
    
  </div>
</template>

<script>
// ======= Libs ========
import axios from 'axios'

// ======= Componentes ========
import Poke from './components/Poke.vue'

export default {
  name: 'App',
  data(){
    return{
      pokemon: [],
      filteredPokemon: [],
      search: ''
    }
  },
  components: {
   Poke
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=1118&offset=0").then(answer =>{
      this.pokemon = answer.data.results
      this.filteredPokemon = answer.data.results
    })
  },
  methods: {
    buscar: function (){
      this.filteredPokemon = this.pokemon
      if(this.search == '' || this.search == ' '){
        this.filteredPokemon = this.pokemon
      } else {
        this.filteredPokemon = this.pokemon.filter(pokemon => pokemon.name == this.search)
      }
  }
  /*computed: {
    searchResult: function (){
      if(this.search == '' || this.search == ' '){
        return this.pokemon
      } else {
        return this.pokemon.name.filter(pokemon => pokemon.name == this.search)
      }
    } */
  } 
}
</script>

<style>
  #app{
    background: black;
    width: 100%;
    height: 100%;
    min-height: 100%;
  }
  #searchPkn{
    margin-left: 50%;
    margin-top: 1rem;
    max-width: 80%;
    min-width: 30%;

    padding: .5rem 1.5rem;

    transform: translateX(-50%);
    cursor: pointer;
    border-radius: 25px;
    border: none;
  }
  #searchPkn:focus{
    border-radius: 25px;;
    outline: none transparent;
    border: 3px solid rgb(101, 202, 233);
    cursor:text;
    transition: border .25s;
  }
  .btnSearch,
  .btnSearch:focus{
    border: none;
    width: 10%;
    max-width: 80%;
    min-width: 10%;
    margin-left: 50%;
    margin-top: 1rem;
    transform: translateX(-50%);
    padding: 1.2rem .5rem;
    outline: none transparent;
    cursor: pointer
  }
  .btnSearch:focus{
    background: rgb(148, 255, 148)
  }
  #column{
    width: 100%;
    box-sizing: border-box;
    padding: 1.5rem 3rem;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    background: black;
  }
  #pokemon{
    margin: 0 0.5rem;
    min-width: 230px;
  }
  .card{
    background: #919191!important;
  }
  @media screen and (max-width: 500px){
    .btnSearch{
      width:25%
    }
  }
</style>
