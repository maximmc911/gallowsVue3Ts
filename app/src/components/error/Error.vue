<template>
  <div class="wrong-letters-container">
    <div class="wrong-letters">
      <p>Ошибки</p>
      <span v-for="(item, index) in props.errorLetter" :key="index">
        {{ `${item}, ` }}
      </span>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  errorLetter: object;
}
const props = defineProps<Props>();
</script>

<style scoped>
.wrong-letters-container {
  position: absolute;
  top: 20px;
  right: 20px;
  display: flex;
  flex-direction: column;
  text-align: right;
}

.wrong-letters-container p {
  margin: 0 0 5px;
}

.wrong-letters-container span {
  font-size: 24px;
}
</style>
