<script setup>
import MemoryCard from './components/MemoryCard.vue';
import HelloTitle from './components/HelloTitle.vue';
import { ref } from 'vue';

const colors = [
  '#ffadad',
  '#ffd6a5',
  '#fdffb6',
  '#caffbf',
  '#9bf6ff',
  '#a0c4ff',
  '#bdb2ff',
  '#ffc6ff',
];

console.log(colors);

const randomColors = [...colors, ...colors].sort(() => Math.random() - 0.5);

const cards = randomColors.map((color, id) => ({ id, color }));

let selectedCards = ref([]);

const handleCardClick = (clickedCard) => {
  if (selectedCards.value.length < 2 && !clickedCard.revealed) {
    selectedCards.value.push(clickedCard);
    clickedCard.isFlipped = true;

    if (selectedCards.value.length === 2) {
      checkMatch();
    }
  }
};

const checkMatch = () => {
  const [card1, card2] = selectedCards.value;

  if (card1.color === card2.color) {
    card1.revealed = true;
    card2.revealed = true;
  } else {
    setTimeout(() => {
      card1.isFlipped = false;
      card2.isFlipped = false;
    }, 1000);
  }

  selectedCards.value = [];
};
</script>

<template>
  <HelloTitle msg="Memory Color Game"></HelloTitle>
  
  <div class="grid grid-cols-4 gap-4">
    <MemoryCard v-for="(card, index) in cards" :key="index" :color="card.color" @click="() => handleCardClick(card)"/>
  </div>

</template>

<style scoped>
@tailwindbase;
@tailwind components;
@tailwind utilities;
</style>
