<script lang="ts" setup>
   import { defineProps } from "vue";

   interface ThingProps{
      choosedThing: string,
   }

   defineProps<ThingProps>()
</script>

<template>
   <div class="rightPlayer">
      <img class="hand" v-if="choosedThing === 'paper'" src="./../../icons/paper.png" alt="paper">
      <img class="hand" v-if="choosedThing === 'scissors'" src="./../../icons/scissors.png" alt="scissors">
      <img class="hand" v-if="choosedThing === 'rock'" src="./../../icons/rock.png" alt="rock">
   </div>
</template>

<style scoped>
   .rightPlayer{
      transform: rotate(180deg);
   }
</style>

