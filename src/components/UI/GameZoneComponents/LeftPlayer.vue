<template>
  <div>
    <img v-if="!props.move" class="hand" src="./../../icons/paper.png" alt="paper">
    <img v-if="props.move === 'paper'" class="hand" src="./../../icons/paper.png" alt="paper">
    <img v-if="props.move === 'scissors'" class="hand" src="./../../icons/scissors.png" alt="scissors">
    <img v-if="props.move === 'rock'" class="hand" src="./../../icons/rock.png" alt="rock">
  </div>
</template>
 
<script lang="ts" setup>
  import { defineProps } from 'vue';
 
  interface BotProps {
    move: string | "paper"
  }
 
  const props = defineProps<BotProps>();
</script>