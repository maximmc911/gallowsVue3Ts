<template>
  <div class="game-container">
    <svg height="250" width="200" class="figure-container">
      <!-- Rod -->
      <line x1="60" y1="20" x2="140" y2="20" />
      <line x1="140" y1="20" x2="140" y2="50" />
      <line x1="60" y1="20" x2="60" y2="230" />
      <line x1="20" y1="230" x2="100" y2="230" />

      <!-- Head -->
      <circle cx="140" cy="70" r="20" />
      <!-- Body -->
      <line x1="140" y1="90" x2="140" y2="150" />
      <!-- Arms -->
      <line x1="140" y1="120" x2="120" y2="100" />
      <line x1="140" y1="120" x2="160" y2="100" />
      <!-- Legs -->
      <line x1="140" y1="150" x2="120" y2="180" />
      <line x1="140" y1="150" x2="160" y2="180" />
    </svg>

    <Error />
    <Letter />
  </div>
</template>

<script setup lang="ts">
import Letter from "../letter/Letter.vue";
import Error from "../error/Error.vue";
</script>

<style scoped>
.game-container {
  padding: 20px 0;
  position: relative;
  margin: auto;
  height: 350px;
}

.figure-container {
  fill: transparent;
  stroke: #3a3a3a;
  stroke-width: 4px;
  stroke-linecap: round;
}

.figure-part {
  display: none;
}
</style>
