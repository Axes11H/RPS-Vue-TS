<script setup lang="ts">
   import Title from "./HeaderComponents/Title.vue";
   import ChooseThing from "./HeaderComponents/ChooseThing.vue";

   function updateChoosedThing(value: string){
      emits('updateChoosedThing', value)
   }

   const emits = defineEmits(['updateChoosedThing', 'startGame'])
</script>

<template>
   <div>
      <Title/>
      <ChooseThing @updateChoosedThing="updateChoosedThing"/>
   </div>
</template>
