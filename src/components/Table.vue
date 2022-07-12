<template>
  <!-- construtor dos itens da tabela -->
  <div class="main-holder">
    <div class="table">
      <div class="pokemon-holder" v-for='(pokemon, index) in filteredPokemons' :key='pokemon.name' @click="showModal = true">
        <span class="id-text">#{{pokemon.id}}</span>
        <img v-bind:src="pokemon.sprites.front_default" alt="">
        <span class="name-text">{{pokemon.name}}</span>
        <div class="types">
          <span class="type"
          v-for="(type, index) in pokemon.types"
          v-bind:style="type.type.name=='normal' ? 'background:#A8A878' :
          type.type.name=='fighting' ? 'background:#C03028' :
          type.type.name=='flying' ? 'background:#A890F0' :
          type.type.name=='poison' ? 'background:#A040A0' :
          type.type.name=='ground' ? 'background:#E0C068' :
          type.type.name=='rock' ? 'background:#B8A038' :
          type.type.name=='bug' ? 'background:#A8B820' :
          type.type.name=='ghost' ? 'background:#705898' :
          type.type.name=='steel' ? 'background:#B8B8D0' :
          type.type.name=='fire' ? 'background:#F08030' :
          type.type.name=='water' ? 'background:#6890F0' :
          type.type.name=='grass' ? 'background:#78C850' :
          type.type.name=='electric' ? 'background:#F8D030' :
          type.type.name=='psychic' ? 'background:#F85888' :
          type.type.name=='ice' ? 'background:#98D8D8' :
          type.type.name=='dragon' ? 'background:#7038F8' :
          type.type.name=='dark' ? 'background:#68A090' :
          type.type.name=='fairy' ? 'background:#EE99AC' :
          type.type.name=='unknown' ? 'background:#68A090' : 
          'background:grey'
          " 
          :key="index">{{type.type.name}}</span>
        </div>
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
        api.get('https://pokeapi.co/api/v2/pokemon/' +p+'').then(response => {
          console.log(response.data)
          
          this.pokemons.push(response.data);           
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
        console.log(+this.pokemons)
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

  .types{
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .type{
    text-transform: uppercase;
    color: #fff;
    padding: 2px 8px;
    margin: 10px 0px;
    border: 1px solid transparent;
    border-radius: 4px;
  }
</style>