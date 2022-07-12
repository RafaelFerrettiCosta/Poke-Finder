<template>
  <!-- ainda não implementado -->
  <div class="modal-overlay">
    <div class="modal">
      <p>Prototipo</p>
      <button>Sair</button>
      <!-- span com background personalizado para cada tipo de pokemon -->
      <!-- <span class="type"
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
          :key="index">{{type.type.name}}</span> -->
    </div>
    <div class="close" @click="$emit('close-modal')">
      <button class="close-img">Fechar</button>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue'

  const isOpen = ref(false)
</script>

<style scoped>
  .modal-overlay {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.2);
    display: none;
  }

  .modal {
    text-align: center;
    background-color: white;
    height: 500px;
    width: 500px;
    margin-top: 10%;
    padding: 60px 0;
    border-radius: 20px;
  }

  .close {
    margin: 10% 0 0 16px;
    cursor: pointer;
  }

  .close-img {
    width: 25px;
  }

  .check {
    width: 150px;
  }


  p {
    font-size: 16px;
    margin: 20px 0;
  }

  button {
    background-color: var(--color-red);
    width: 150px;
    height: 40px;
    color: white;
    font-size: 14px;
    border-radius: 16px;
    margin-top: 50px;
  }
</style>