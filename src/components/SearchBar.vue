<template>
  <div class="main-holder">
    <div class="text-filter">
      <input class="search-box" type="text" v-model='search' placeholder="Procurar...">
    </div>

    <div class="options">
      <div class="container-orderby filter">
        <label for="order-by">Ordenar por</label>
        <select name="type" id="type">
          <option value="id">ID [Menor-Maior]</option>
          <!-- <option value="rev-id">ID [Maior-Menor]</option>
          <option value="name">Nome [A-Z]</option>
          <option value="rev-name">Nome [Z-A]</option> -->
        </select>
      </div>




    </div>
    <Table :text="search" />
  </div>
</template>

<script>
  import Table from './Table';
  import api from '../services/api';

  export default {
    name: 'SearchBar',
    components: {
      Table,
    },
    data() {
      return {
        search: ''
      }
    },
    mounted() {
      api.get('https://pokeapi.co/api/v2/type/').then(response => {
        console.log(response.data.results);
        this.types = (response.data.results);
      });
      api.get('https://pokeapi.co/api/v2/generation/').then(response => {
        console.log(response.data.results);
        this.gens = (response.data.results);
      });
    }
  }
</script>

<style scoped>
  .main-holder {
    width: 100%;
    display: grid;
    justify-content: center;
    align-items: center;
    gap: 20px;
    margin-top: 20px;
  }

  .text-filter {
    display: flex;
    align-content: center;
    justify-content: center;
  }

  .search-box {
    font-size: 1.25rem;
    padding: 5px 5px 5px 15px;
    border: 1px solid lightgray;
    border-radius: 20px;
  }

  .button-img {
    max-width: 20px;
  }

  .options {
    max-width: 1000px;
    margin: 0 auto;
    flex-wrap: nowrap;
  }

  option {
    text-transform: capitalize;
  }



  .filter label {
    margin-right: 10px;
  }
</style>