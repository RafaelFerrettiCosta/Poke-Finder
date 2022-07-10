<template>
  <div class="main-holder">
    <div class="text-filter">
      <input class="search-box" type="text" placeholder="Procurar...">
      <button class="search-button">
        <img class="button-img" src="../assets/lupa.png" alt="">
      </button>
    </div>

    <div class="options">
      <div class="container-type filter">
        <label for="type">Tipo</label>
        <select name="type" id="type">
          <option value="rock">Todos</option>
          <option value="rock">Pedra</option>
          <option value="rock">Fada</option>
        </select>
      </div>

      <div class="container-gen filter">
        <label for="generation">Geração</label>
        <select name="type" id="type">
          <option value="rock">Todas</option>
          <option value="gen-1">Gen I</option>
          <option value="gen-2">Gen II</option>
          <option value="gen-3">Gen III</option>
          <option value="gen-4">Gen IV</option>
          <option value="gen-5">Gen V</option>
          <option value="gen-6">Gen VI</option>
          <option value="gen-7">Gen VII</option>
          <option value="gen-8">Gen VIII</option>
          <option value="gen-9">Gen IX</option>
          <option value="gen-10">Gen X</option>
        </select>
      </div>

      <div class="container-orderby filter">
        <label for="order-by">Ordenar por</label>
        <select name="type" id="type">
          <option value="name">Nome [A-Z]</option>
          <option value="rev-name">Nome [Z-A]</option>
          <option value="id">ID [Menor-Maior]</option>
          <option value="rev-id">ID [Maior-Menor]</option>
        </select>
      </div>




    </div>
  </div>
</template>

<script>
  export default {
    name: 'SearchBar'
  }
</script>

<style scoped>
  .main-holder {
    width: 100%;
    padding: 10px 50px;
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
    border-top-left-radius: 20px;
    border-bottom-left-radius: 20px;
  }

  .search-button {
    background-color: var(--color-red);
    border: none;
    border: 5px solid var(--color-red);
    border-bottom-right-radius: 30px;
    border-top-right-radius: 30px;
    padding-right: 5px;
  }

  .button-img {
    max-width: 20px;
  }

  .options {
    display: flex;
    justify-content: space-between;
    gap: 80px;
  }



  .filter
  label {
    margin-right: 10px;
  }
</style>