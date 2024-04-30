<script setup lang="ts">
   import { ref } from "vue";

   import Header from './UI/Header.vue';
   import GameZone from './UI/GameZone.vue';

   let choosedThing = ref<string>("");

   function updateChoosedThing(value: string){
      choosedThing.value = value;
   }
</script>

<template>
   <div class="container">
      <Header @updateChoosedThing="updateChoosedThing"/>
      <GameZone :choosedThing="choosedThing" class="mt-5"/>
   </div>
</template>