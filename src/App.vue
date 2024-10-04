<template>
  <div id="app">
    <NavBar></NavBar>
    <PokeSearch></PokeSearch>
  </div>
</template>

<script>

import NavBar from './components/NavBar.vue';
import PokeSearch from './components/PokeSearch.vue';
export default {
  name: 'App',
  components: {
    PokeSearch ,
    NavBar
  }
}
</script>

<style>

</style>
