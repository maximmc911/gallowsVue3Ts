<template>
  <div id="app">
    <Header />
    <Figure />
  </div>
</template>

<script setup lang="ts">
import Header from "./components/header/Header.vue";
import Figure from "./components/figure/Figure.vue";
</script>

<style>
#app {
  max-width: 450px;
  width: 100%;
  padding: 20px 30px;
  box-sizing: border-box;
}
</style>
