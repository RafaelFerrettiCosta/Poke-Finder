<template>
  <div class="main-holder">
    <button @click="isOpen = true">Open</button>
      <div class="modal" v-if="isOpen">
        <h2>titulo</h2>
        <p>info</p>
        <button @click="isOpen = false">Close</button>
      </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue'

  const isOpen = ref(false)
</script>

<style scoped>
  .main-holder {
    position: relative;
  }

  .modal {
    position: absolute;
    top: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.1);
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal div {
    background-color: var(--color-white);
    padding: 50px;
    border-radius: 10px;
  }
</style>