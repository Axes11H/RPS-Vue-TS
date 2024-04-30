<script setup lang="ts">
import { defineProps, ref, onMounted } from "vue";

import LeftPlayer from "./GameZoneComponents/LeftPlayer.vue";
import RightPlayer from "./GameZoneComponents/RightPlayer.vue";
import SelfScore from "./GameZoneComponents/SelfScore.vue";
import Timer from "./GameZoneComponents/Timer.vue";
import ButtonStart from "./HeaderComponents/ButtonStart.vue";

interface ThingProps {
  choosedThing: String;
}

let playerName = ref<string>("Player");
let editingName = ref<boolean>(false);
let botMoveResult = ref<number | null>(null); // Сохраняем результат хода бота

const timerComponentRef = ref();

function editName() {
  editingName.value = true;
}

function saveName() {
  editingName.value = false;

  localStorage.setItem("playerName", playerName.value);
}

function startGame() {
  botMoveResult.value = botMove();
  console.log(botMoveResult.value)
  timerComponentRef.value?.startTimer();
}

function botMove() {
  return Math.floor(Math.random() * (4 - 1) + 1); 
}

onMounted(() => {
  playerName.value = localStorage.getItem("playerName") || "Player";
});

defineProps<ThingProps>();
</script>

<template>
  <ButtonStart @click="startGame" />
  <div class="d-flex justify-content-between align-items-center">
    <div class="playerBox">
      <SelfScore name="Bot" score="0" />
      <LeftPlayer :move="botMoveResult" />
    </div>
    <div>
      <Timer ref="timerComponentRef" />
    </div>
    <div class="playerBox">
      <div v-if="editingName" class="d-flex align-items-center gap-2 pointer">
        <img class="editName" src="./../icons/pencil.png" alt="edit Name" @click="editName" />
        <input v-model="playerName" type="text" class="fs-3" @keydown.enter="saveName" @blur="saveName" />
      </div>
      <div v-else class="d-flex align-items-center gap-2 pointer">
        <img class="editName" src="./../icons/pencil.png" @click="editName" alt="edit Name" />
        <SelfScore :name="playerName" score="0" />
      </div>
      <RightPlayer :choosedThing="choosedThing || 'paper'" />
    </div>
  </div>
</template>

<style scoped>
.playerBox {
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 30px;
}
</style>
