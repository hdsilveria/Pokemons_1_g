<template>
<div id="app">

  <div class="w3-top">
    <div class="w3-bar" id="menu">
      <div class="w3-center">
        <input type="text" placeholder="Buscar Pokémon" v-model="busca">
        <button class="w3-button w3-white w3-hover-white w3-margin w3-border w3-border-grey" @click="buscar"> Buscar</button>
      </div>
    </div>
  </div>


<div id="pokens">
  <header>
    <br><h3><img src="./assets/poke.png" alt="">Pokémons 1° Geração</h3><br>
  </header>

<div id="notFound" v-show="NotFound" class="w3-tag w3-red">
  <h2>Não encontrado 💥 </h2>
</div>

<div class="card-group row row-cols-2 row-cols-md-5">
    <div v-for="poke in buscaResults" :key="poke.url">
        <pokemon :name="poke.name" :url="poke.url" />
    </div>
</div>

</div>

<footer>
  <hr><p>Desenvolvido por &copy;Henrique_Duarte</p>
</footer>

</div>
</template>

<script>

import axios from 'axios';
import pokemon from './components/pokemon'

export default {
  data(){
    return {
      pokemons: [],
      buscaResults: [],
      busca: [],
      NotFound: false
    }
  },

  name: 'App',

  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(response =>{
      this.pokemons = response.data.results;
      this.buscaResults = response.data.results;
          console.log(this.pokemons);
    })
  },

  components: {
    pokemon
  },

  methods:{
    buscar: function(){
      this.buscaResults = this.pokemons,
      this.NotFound = false;

      if (this.busca == "" || this.busca == null){
        this.buscaResults = this.pokemons.data.results
      }
        this.buscaResults = this.pokemons.filter(pokemon => pokemon.name == this.busca)

      if (this.buscaResults == '' || this.buscaResults == null){
          this.NotFound = true
      }
        this.busca = '';
    }

  }

}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
  color: rgb(97, 97, 97);
}

#pokens {
  margin: 5%;
  margin-top: 70px;
}

#menu {
  background-color: rgba(240, 236, 3, 0.904);
  color: white;
}

body {
  background-color: rgb(255, 254, 205);
}

#notFound {
  transform: rotate(-5deg); 
  margin: 70px;
  padding: 2%;
}

</style>
