<script lang="ts">
   import { defineComponent } from 'vue';

   export default defineComponent({
      props: {
         score: {
            type: Number,
            reqiered: true
         }
      }
   })
</script>

<template>
   <div class="text-center fs-3 mt-3 fw-bold">Score : {{ score || 0 }}</div>
</template>