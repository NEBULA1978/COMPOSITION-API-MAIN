<template>
  <div>
    <OptionApi />
    <CompositonApiOpcionUno />
    <CompositonApiOpcionDos />
  </div>
</template>

<script setup>
  import OptionApi from './components/OptionApi.vue'
  import CompositonApiOpcionUno from './components/CompositonApiOpcionUno.vue'
  import CompositonApiOpcionDos from './components/CompositionApiOpcionDos.vue'
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
