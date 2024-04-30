<template>
   <div>
     <img v-if="displayMove === 1" class="hand" src="./../../icons/paper.png" alt="paper">
     <img v-if="displayMove === 2" class="hand" src="./../../icons/scissors.png" alt="scissors">
     <img v-if="displayMove === 3" class="hand" src="./../../icons/rock.png" alt="rock">
   </div>
 </template>
 
 <script lang="ts" setup>
   import { defineProps, ref } from 'vue';
 
   interface BotProps {
     move: number | 1
   }
 
   const props = defineProps<BotProps>();
 
   const displayMove = ref<number>();
 
   setTimeout(() => {
     displayMove.value = props.move;
   }, 4500);
 </script>
 