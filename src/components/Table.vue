<template>
  <!-- construtor dos itens da tabela -->
  <div class="main-holder">
    <div class="button-holder">
      <!-- ao clicar no botão chama função setIndex que por sua vez altera o valor que local storage procura -->
      <!-- adicionando um v-if para adicionar 0 aos valores de 1 digito -->
      <button class="page-button" v-for="index in pagesCount" v-if="index<10" @click="setIndex(index)">0{{index}}</button>
      <button class="page-button" v-for="index in pagesCount" v-if="index>=10" @click="setIndex(index)">{{index}}</button>

    </div>
    <div class="table">
      <!-- cada pokemon é carregado a partir da primeira camada da API, extraindo o ID de cada a partir da URL -->
      <div class="pokemon-holder" v-for='(pokemon, index) in filteredPokemons' :key='pokemon.name' @click="showModal = true">
        <span class="id-text">#{{pokemon.url.slice(34,-1)}}</span>
        <img v-bind:src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+pokemon.url.slice(34,-1)+'.png'" @error="setAltImg" alt="">
        <span class="name-text">{{pokemon.name}}</span>
        <div class="types">
        </div>
        <DetailsModal v-show="showModal" @close-modal="showModal=false" />

      </div>
    </div>
  </div>
</template>

<script>
  import api from '../services/api'
  import DetailsModal from './DetailsModal'
  export default {
    name: 'Table',
    props: ["text"],
    components: {
      DetailsModal
    },
    methods: {
      setIndex: function (i) {
        this.index = i;
      },
      setAltImg(event) {
        // event.target.src = "../assets/pokeapi.png"
      }
    },
    data() {
      return {
        pokemons: [],
        counter: [],
        showModal: false,
        pagesCount: 12,
        index: 1
      }
    },
    mounted() {
      async function montarLocalStorage() {
        var page = 1
        let result = await api.get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=100')
        var next = await result.data.next;
        localStorage.setItem("pokelist" + page, JSON.stringify(result.data.results))
        while (next !== null) {
          page++;
          result = await api.get(next)
          next = await result.data.next;
          localStorage.setItem("pokelist" + page, JSON.stringify(result.data.results))
        }
      }
      montarLocalStorage();
      this.pagesCount = localStorage.length;
      console.log(this.pagesCount)

    },
    computed: {
      // filtro para a barra de pesquisa aceitar tanto nome quanto ID's
      filteredPokemons: function () {
        if (this.pagesCount !== localStorage.length) {
          setTimeout(function () {
            window.location.reload(1);
          }, 1000);
        }
        this.pokemons = localStorage.getItem("pokelist" + this.index)
        this.pokemons = JSON.parse(this.pokemons || '[]')
        var pokeID = ''

        return this.pokemons.filter((pokemon) => {
          pokeID = (pokemon.url.slice(34, -1))
          return pokemon.name.match(this.text) || JSON.stringify(pokeID).match(this.text);
          this.pagesCount = localStorage.length
        });
      }
    }

  }
</script>

<style scoped>
  img {
    max-width: 200px;
    margin: 15px;
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

  .pokemon-holder:hover {
    cursor: pointer;
  }

  .name-text {
    font-size: 1.2rem;
    margin-top: -20px;
    text-transform: capitalize;
  }

  .id-text {
    font-size: 1.4rem;
    position: absolute;
    right: 10px;
    top: 8px;
  }

  .types {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .type {
    text-transform: uppercase;
    color: #fff;
    padding: 2px 8px;
    margin: 10px 0px;
    border: 1px solid transparent;
    border-radius: 4px;
  }

  .button-holder {
    width: 100%;
    display: flex;
    align-content: center;
    justify-content: center;
    gap: 20px;
  }

  .page-button {
    padding: 5px 10px;
    background: var(--color-red);
    color: white;
    border: 2px solid var(--color-white);
    border-radius: 4px;
  }

  .page-button:hover {
    cursor: pointer;
  }
</style>