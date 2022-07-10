<template>
  <div class="main-holder">
    <div class="table">
      <div class="pokemon-holder" v-for='(pokemon, index) in pokemons' :key='pokemon.name'>
        <span class="id-text">#{{pokemon.id}}</span>
        <img v-bind:src="pokemon.sprites.front_default" alt="">
        <span class="name-text">{{pokemon.name}}</span>
        <DetailsModal/>
      </div>
    </div>
  </div>
</template>

<script>
  import api from '../services/api'
  import DetailsModal from './DetailsModal'
  export default {
    name: 'Table',
    components: {
      DetailsModal
    },
    data() {
      return {
        pokemons: []
      }
    },
    mounted() {
      for (var p = 1; p <= 20; p++) {
        api.get('https://pokeapi.co/api/v2/pokemon/' + p).then(response => {
          console.log(response.data);
          this.pokemons.push(response.data)
          localStorage.setItem('pokelist', JSON.stringify(response.data))
        })
      }

    }

  }
</script>

<style scoped>
  img {
    max-width: 200px;
  }

  .main-holder {
    max-width: 1000px;
    margin: 30px 20px;
  }

  .table {
    width: 100%;
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