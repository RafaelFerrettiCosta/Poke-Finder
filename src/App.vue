<template>
  <div id="app">
    <Header />
    <main class="content-holder">
      <SearchBar />
      <Table />
    </main>
  </div>
</template>

<script>
import './styles/global.css';

import Header from './components/Header';
import SearchBar from './components/SearchBar';
import Table from './components/Table';

export default {
  name: 'App',
  components: {
    Header,
    SearchBar,
    Table
  }
}
</script>

<style scoped>
  .content-holder{
  display: grid;
  max-width: 1000px;
  margin: 0 auto;
  background-color: var(--color-white);
  border: 1px solid var(--color-white);
  border-radius: 4px;
  margin-top: 50px;    
  }
</style>

