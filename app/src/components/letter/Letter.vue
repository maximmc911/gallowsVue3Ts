<template>
  <div class="word">
    <span class="letter">л</span>
    <span class="letter"></span>
    <span class="letter">д</span>
    <span class="letter"></span>
    <span class="letter"></span>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped>
.word {
  display: flex;
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
}

.letter {
  border-bottom: 3px solid #54bc6c;
  display: inline-flex;
  font-size: 30px;
  align-items: center;
  justify-content: center;
  margin: 0 3px;
  height: 50px;
  width: 20px;
}
</style>
