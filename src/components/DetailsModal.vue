<template>
  <div class="modal-overlay">
    <div class="modal">
      <p>Prototipo</p>
      <button>Sair</button>
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