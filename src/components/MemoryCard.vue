<template>
    <div class="memory-card" :class="{ flipped: card.isFlipped }" @click="flipCard">
         <div  class="card-face front" ></div>
         <div  class="card-face back specific-back" :style="{backgroundColor: card.isFlipped ? color : '' }"></div>
    </div>
 </template>
 
 <script setup>
     import { ref, reactive, defineProps } from 'vue';
 
    const props = defineProps(['color'])

    const card = reactive({
        isFlipped: ref(false),
    });

    const flipCard = () => {
        card.isFlipped = !card.isFlipped;
    };
 </script>
 
 <style scoped>
 
     .memory-card {
         width: 100px;
         height: 100px;
         background-color: #be0404;
         border-radius: 5px;
         perspective: 1000px;
         cursor: pointer;
     }
 
     .memory-card .card-face {
         width: 100%;
         height: 100%;
         backface-visibility: hidden;
         border-radius: 5px;
         position: absolute;
         transition: transform 0.6s, background-color 0.6s;
     }
 
     .memory-card .front {
         background-color: #d40606;
         transform: rotateY(0deg);
     }
 
     .memory-card .back {
         transform: rotateY(180deg);
     }
 
     .memory-card.flipped .front {
         transform: rotateY(-180deg);
     }
 
     .memory-card.flipped .specific-back {
         transform: rotateY(0deg);
     }
 </style>