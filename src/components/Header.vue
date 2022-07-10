<template>
  <header>
    <img src="../assets/Pokemon_logo.svg" alt="">
  </header>
</template>

<script>
  export default {
    name: 'Header'
  }
</script>

<style scoped>
  header {
    display: grid;
    position: relative;
    width: 100%;
    padding: 10px 20px;
    background-color: var(--color-white);
    justify-items: center;

  }
  img {
    max-width: 200px;
  }

</style>