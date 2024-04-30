<script setup lang="ts">
   interface SelfScoreProps{
      name: String,
      score: Number
   }

   defineProps<SelfScoreProps>()
</script>

<template>
   <div class="fs-3">{{ name }} : {{ score }}</div>
</template>