<template>
  <div class="main-holder">
    <div class="desc">
      <h3>Rafael Ferretti Costa</h3>
      <span class="short-t">Desenvolvedor e Analista de Dados</span>
      <div class="flex-line">
        <a href="https://www.github.com/RafaelFerrettiCosta/"><img class="tag-git" src="../assets/git.png" alt=""></a>
        <a href="https://www.linkedin.com/in/rafael-ferretti/"><img class="tag-link" src="../assets/linkedin.png" alt=""></a>
      </div>




    </div>
    <div class="thanks-to">
      <span class="short-t">Powered by</span>
      <div class="links">
        <a href="https://binds.co" target="_blank">
          <img class="binds" src="../assets/bindsco.svg" alt="">
        </a>
        <a href="https://pokeapi.co" target="_blank">
          <img class="binds" src="../assets/pokeapi.png" alt="">
        </a>
      </div>

    </div>

  </div>



</template>

<script>
  export default {
    name: 'Footer'
  }
</script>

<style scoped>
  .binds {
    max-width: 120px;
  }

  .tag-link {
    max-width: 53px;
  }

  .tag-git {
    max-width: 40px;
  }

  .main-holder {
    background-color: var(--color-white);
    display: grid;
    grid-template-columns: 3fr 1fr;
    padding: 20px 0px 20px 20px;
  }

  .short-t {
    font-style: italic;
  }

  .flex-line {
    display: flex;
    align-items: center;
  }

  .thanks-to {
    align-self: center;
  }

  .links {
    display: flex;
    align-items: center;
    gap: 5px;
  }
</style>