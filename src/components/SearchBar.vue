<template>
  <div class="main-holder">
    <div class="text-filter">
      <input class="search-box" type="text" v-model='search' placeholder="Procurar...">
    </div>

    <div class="options">
      <div class="container-type filter">
        <label for="type">Tipo</label>
        <select name="type" id="type">
          <option value="">Todos</option>
          <option v-for="t in types" :key="t.name" :value="t.name">{{t.name}}</option>
        </select>
      </div>

      <div class="container-gen filter">
        <label for="generation">Geração</label>
        <select name="type" id="generation">
          <option value="">Todas</option>
          <option v-for="g in gens" :key="g.name" :value="g.name">{{g.name}}</option>
        </select>
      </div>

      <div class="container-orderby filter">
        <label for="order-by">Ordenar por</label>
        <select name="type" id="type">
          <option value="id">ID [Menor-Maior]</option>
          <option value="rev-id">ID [Maior-Menor]</option>
          <option value="name">Nome [A-Z]</option>
          <option value="rev-name">Nome [Z-A]</option>
        </select>
      </div>




    </div>
    <Table :text="search" :type="type" :gen="gen" />
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
        search: '',
        type: 'Todos',
        gen: 'Todas',
        types: [],
        gens: []
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
    display: flex;
    justify-content: space-between;
    gap: 80px;
    flex-wrap: nowrap;
  }

  option {
    text-transform: capitalize;
  }



  .filter label {
    margin-right: 10px;
  }
</style>