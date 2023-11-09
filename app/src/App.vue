<template>
  <div id="app">
    <Header />
    <Figure />
    <Notification />
  </div>
</template>

<script setup lang="ts">
/* 
import  Modal  from './components/modalWindow/Modal.vue' 
<Modal/>
 */

import Header from "./components/header/Header.vue";

import Figure from "./components/figure/Figure.vue";
import Notification from "./components/notification/Notification.vue";
</script>

<style>
#app {
  max-width: 450px;
  width: 100%;
  padding: 20px 30px;
  box-sizing: border-box;
}
</style>
