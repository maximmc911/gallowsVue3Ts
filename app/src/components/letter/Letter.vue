<script setup lang="ts">
interface Props {
  word: string;
  correctLetters: string[];
}

const props = defineProps<Props>();
</script>
<template>
  <div class="word">
    <span class="letter" v-for="(item, index) in props.word" :key="index">
      {{ props.correctLetters.includes(item) ? item : `` }}
    </span>
    <div></div>
  </div>
</template>

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
