<script lang="ts" setup>
   import { defineProps } from "vue";
    
   interface BtnProps{
      text: string
   }

   const props = defineProps<BtnProps>()
</script>

<template>
   <button>{{ props.text }}</button>
</template>

<style scoped>
   button{
      padding: 15px 100px;
      border: 2px solid black;
      outline: none;
      background-color: transparent;
   }

   button:hover{
      background-color: black;
      color: white;
   }
</style>