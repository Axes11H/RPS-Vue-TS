<script setup lang="ts">
   import { defineComponent, defineProps } from "vue";

   import Title from "./HeaderComponents/Title.vue";
   import AllScore from "./HeaderComponents/AllScore.vue"
   import ChooseThing from "./HeaderComponents/ChooseThing.vue";

   function updateChoosedThing(value: string){
      emits('updateChoosedThing', value)
   }


   const emits = defineEmits(['updateChoosedThing', 'startGame'])
</script>

<template>
   <div>
      <Title/>
      <AllScore/>

      <ChooseThing @updateChoosedThing="updateChoosedThing"/>
   </div>
</template>
