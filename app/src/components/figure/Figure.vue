<template>
  <div class="game-container">
    <svg height="250" width="200" class="figure-container">
      <!-- Rod -->
      <line x1="60" y1="20" x2="140" y2="20" />
      <line x1="140" y1="20" x2="140" y2="50" />
      <line x1="60" y1="20" x2="60" y2="230" />
      <line x1="20" y1="230" x2="100" y2="230" />
      <!-- Head -->
      <circle cx="140" cy="70" r="20" v-if="errorLetter.length >= 1" />
      <!-- Body -->
      <line x1="140" y1="90" x2="140" y2="150" v-if="errorLetter.length >= 2" />
      <!-- Arms -->
      <line x1="140" y1="120" x2="120" y2="100"  v-if="errorLetter.length >= 3"/>
      <line x1="140" y1="120" x2="160" y2="100"  v-if="errorLetter.length >= 4"/>
      <!-- Legs -->
      <line x1="140" y1="150" x2="120" y2="180" v-if="errorLetter.length >= 5" />
      <line x1="140" y1="150" x2="160" y2="180" v-if="errorLetter.length >= 6"/>
    </svg>

    <Error 
    :errorLetter ="errorLetter"
    />
  
    <Letter :word="word" :correctLetters="correctLetters" />
    <Notification ref="visible" />
    <Modal ref="open" :word="word" @restart="restart"/>
  </div>
</template>

<script setup lang="ts">
import Letter from "../letter/Letter.vue";
import Error from "../error/Error.vue";
import Notification from "../notification/Notification.vue";
import  Modal  from '../modalWindow/Modal.vue' 
import { ref, computed, watchEffect, watch} from "vue";
import axios from 'axios'
const word = ref(``);
const block = ref<boolean>(true)
const visible = ref<InstanceType<typeof Notification>|null>(null);
const open = ref<InstanceType<typeof Modal>|null>(null);
    let uniqueLetter : string[] = [];
  const dowbbleWord : string[] = [];
const getName = async () =>{
  try {
    const {data} = await axios<{FirstName: string}>(`https://api.randomdatatools.ru/?unescaped=false&params=FirstName`);
    word.value = data.FirstName.toLowerCase();
    console.log(data.FirstName);
    for (let index = 0; index < word.value.length; index++) {
      console.log(word.value[index]);
      
      dowbbleWord.push(word.value[index])
    }
    
    const newSet : any = new Set(dowbbleWord);
    uniqueLetter = Array.from(newSet)
  } catch (error) {
    word.value=``;
  }
  

}
getName()
const letters = ref<string[]>([]);
window.addEventListener(`keydown`, ({ key }) => {
  if (block.value) {
    if (letters.value.includes(key)) {
      visible.value?.open();
  
      setTimeout(() => visible.value?.close(), 2000);
    }else if (/[а-яА-ЯёЁ]/.test(key)) {
      letters.value.push(key.toLowerCase());
    }
  }
});

const correctLetters = computed(() =>
  letters.value.filter((x) => word.value.includes(x))
);
const errorLetter = computed(() => letters.value.filter(x => !word.value.includes(x)) )

/* watchEffect(() => {



  
}) */
watch(errorLetter, () => {
  if (errorLetter.value.length == 6) {
    console.log(`рабоатет`);
    open.value?.isVisible( `lose`);
    block.value = false;

  }
})
watchEffect(() => {

  if (uniqueLetter.length !== 0 || correctLetters.value.length !==0) {
    console.log(`работает1`);
    
    if (uniqueLetter.length === correctLetters.value.length) {
      console.log(`работает2`);
      open.value?.isVisible( `win`);
      block.value = false;
    }
    console.log(`работает3`);
  }

})
/* watch(uniqueLetter , () => {
}) */
const restart = async () =>{
  uniqueLetter.length =0;
  dowbbleWord.length = 0;
  console.log(uniqueLetter);
  
  await getName(); 
  letters.value = [];
  open.value?.noVisible();
  block.value =true;

}

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
