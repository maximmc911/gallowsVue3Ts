<template>
  <!-- Notification -->
  <div class="notification-container" :class="{ show: isVisible }">
    <p>Вы уже вводили эту букву</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const isVisible = ref<boolean>(false);

const close = () => {
  isVisible.value = false;
};
const open = () => {
  isVisible.value = true;
};
defineExpose({ open, close });
</script>

<style scoped>
.notification-container {
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 10px 10px 0 0;
  padding: 15px 20px;
  position: absolute;
  bottom: -150px;
  transition: transform 0.3s ease-in-out;
}

.notification-container p {
  margin: 0;
}

.notification-container.show {
  transform: translateY(-150px);
}
</style>
