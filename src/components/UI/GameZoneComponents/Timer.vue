<script setup lang="ts">
   import { ref } from "vue";

   let countdown = ref<number>(3);
   let showTimerValue = ref<boolean>(false)

   function startTimer(){
      countdown.value = 3;

      showTimer();

      const timer = setInterval(() => {
         if (countdown.value > 0) {
            countdown.value -= 1;
         } else {
            clearInterval(timer);
         }
      }, 1000);
   }

   function showTimer(){
      showTimerValue.value = true;
      let show = setTimeout(() => {
         showTimerValue.value = false;
      }, 3500)
   }

   defineExpose({
      startTimer
   })
</script>

<template>
   <div v-if="showTimerValue" class="fs-1">
      {{ countdown }}
   </div>
</template>