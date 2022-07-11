<template>
  <!-- construtor dos itens da tabela -->
  <div class="main-holder">
    <div class="table">
      <div class="pokemon-holder" v-for='(pokemon, index) in filteredPokemons' :key='pokemon.name' @click="showModal = true">
        <span class="id-text">#{{pokemon.id}}</span>
        <img v-bind:src="pokemon.sprites.front_default" alt="">
        <span class="name-text">{{pokemon.name}}</span>
          <DetailsModal v-show="showModal" @close-modal="showModal=false"/>

      </div>
    </div>
  </div>
</template>

<script>
  import api from '../services/api'
  import DetailsModal from './DetailsModal'
  export default {
    name: 'Table',
    props: ["text","type","gen"],
    components: {
      DetailsModal
    },
    data() {
      return {
        pokemons: [],
        counter:[],
        showModal: false
      }
    },
    mounted() {
      //loop feito para acessar a 'camada especifica' de cada pokemon na API
      api.get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=9999').then(response => {
        this.counter=response.data.results
        // this.counter.length
      }).then(r =>{
        for (var p = 1; p <= 50; p++) {
        api.get('https://pokeapi.co/api/v2/pokemon/' + p).then(response => {
          this.pokemons.push(response.data) 
          
          localStorage.pokemonList = JSON.stringify(this.pokemons);   
        })
      }
      })
      // console.log(this.pokemons)
      // localStorage.setItem("pokelist", JSON.stringify(this.pokemons))


    },
    // filtro para a barra de pesquisa aceitar tanto nome quanto ID's
    computed: {
      filteredPokemons: function(){
        return this.pokemons.filter((pokemon) =>{
          return pokemon.name.match(this.text) || JSON.stringify(pokemon.id).match(this.text);
        });
      }
    }

  }
</script>

<style scoped>
  img {
    max-width: 200px;
  }

  .main-holder {
    margin: 30px 20px;
  }

  .table {
    width: 700px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 20px;
  }

  .pokemon-holder {
    position: relative;
    display: grid;
    border: 2px solid lightgrey;
    border-radius: 8px;
    max-width: 600px;
    justify-items: center;
    box-shadow: 2px 5px grey;
  }

  .pokemon-holder:hover{
    cursor: pointer;
  }

  .name-text {
    font-size: 1.2rem;
    margin-top: -20px;
    text-transform: capitalize;
  }

  .id-text{
    font-size: 1.4rem;
    position: absolute;
    right: 10px;
    top: 8px;
  }
</style>