<script setup lang="ts">
   import { ref, defineEmits } from "vue"

   let choosedThing = ref<string>("")
   
   function choosething(value: string){
      choosedThing.value = value

      emits('updateChoosedThing', value);
   }

   function isStringSelected(value: string) {
      return choosedThing.value === value;
   }

   const emits = defineEmits(['updateChoosedThing']);

</script>

<template>
   <div class="things mt-5 d-flex justify-content-center">
      <button @click="choosething('rock')" :class="{ 'highlight': isStringSelected('rock')}">ROCK</button>
      <button @click="choosething('paper')" :class="{ 'highlight': isStringSelected('paper')}">PAPER</button>
      <button @click="choosething('scissors')" :class="{ 'highlight': isStringSelected('scissors')}">SCISSORS</button>
   </div>
</template>

<style scoped>
   button{
      display: flex;
      align-items: center;
      justify-content: center;
      width: 300px;
      height: 60px;
      border: none;
      border-bottom: 1px solid black !important;
      outline: none;
      background-color: transparent;
   }

   button:hover{
      background-color: black;
      color: white;
   }

   .highlight{
      background-color: black;
      color: white;
   }
</style>