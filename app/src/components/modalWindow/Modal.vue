<template>
  <!-- Container for final message -->
  <div class="popup-container" :class="{ active: open }">
    <div class="popup">
      <div v-if="gameStatus == `win`">
        <h2>Поздравляю, вы победили! 😃</h2>
      </div>
      <div v-if="gameStatus == `lose`">
        <h2>Вы проиграли. 😕</h2>
        <h3>...имя: {{ props.word }}</h3>
      </div>
      <button @click="emit('restart')">Сыграть еще раз</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { Status } from "../interface/type";
interface Props {
  word: string;
}
const props = defineProps<Props>();
const open = ref<boolean>(false);
const gameStatus = ref<Status | null>(null);

const isVisible = (status: Status) => {
  open.value = true;
  gameStatus.value = status;
};
const noVisible = () => {
  open.value = false;
};
defineExpose({
  isVisible,
  noVisible,
});
const emit = defineEmits<{
  (e: "restart"): void;
}>();
</script>

<style scoped>
.popup-container {
  background-color: rgba(0, 0, 0, 0.3);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: none;
  align-items: center;
  justify-content: center;
}

.popup {
  background: #54bc6c;
  border-radius: 5px;
  box-shadow: 0 15px 10px 3px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: center;
}

.popup h2,
.popup h3 {
  color: #fff;
}

.popup button {
  cursor: pointer;
  background-color: #fff;
  color: #54bc6c;
  border: 0;
  margin-top: 20px;
  padding: 12px 20px;
  font-size: 16px;
}

.popup button:active {
  transform: scale(0.98);
}

.popup button:focus {
  outline: 0;
}
.popup-container.active {
  display: flex;
}
</style>
