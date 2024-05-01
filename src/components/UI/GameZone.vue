<script setup lang="ts">
import { defineProps, ref, onMounted } from "vue";

import LeftPlayer from "./GameZoneComponents/LeftPlayer.vue";
import RightPlayer from "./GameZoneComponents/RightPlayer.vue";
import SelfScore from "./GameZoneComponents/SelfScore.vue";
import Timer from "./GameZoneComponents/Timer.vue";
import ButtonStart from "./HeaderComponents/ButtonStart.vue";

interface ThingProps {
  choosedThing: string;
}

let playerName = ref<string>("Player");
let editingName = ref<boolean>(false);
let botMoveResult = ref<string>("");

let playerScore = ref<number>(0);
let botScore = ref<number>(0);

const timerComponentRef = ref();

function editName() {
  editingName.value = true;
}

function saveName() {
  editingName.value = false;
  localStorage.setItem("playerName", playerName.value);
}

function startGame() {
  timerComponentRef.value?.startTimer();

  setTimeout(() => {
    botMoveResult.value = botMove();
    makeResult(botMoveResult.value, props.choosedThing)
  }, 3500)
}

function restartGame(){
  playerScore.value = 0;
  botScore.value = 0;

  localStorage.removeItem("botScore");
  localStorage.removeItem("playerScore");
}

function makeResult(bot:string, player:string){
  if (player === bot) {
      botScore.value += 1;
      playerScore.value += 1;
    } else if (
        (player === "rock" && bot === "scissors") ||
        (player === "scissors" && bot === "paper") ||
        (player === "paper" && bot === "rock")
    ) {
        playerScore.value += 1
    } else {
        botScore.value += 1
    }
    localStorage.setItem("playerScore", playerScore.value.toString())
    localStorage.setItem("botScore", botScore.value.toString())
}

function botMove() {
  let num = Math.floor(Math.random() * (4 - 1) + 1); 

  if(num === 1){
    return botMoveResult.value = "paper"
  }else if(num === 2){
    return botMoveResult.value = "scissors"
  }else{
    return botMoveResult.value = "rock"
  }
} 

onMounted(() => {
  playerName.value = localStorage.getItem("playerName") || "Player";

  const playerScoreString = localStorage.getItem("playerScore");
  playerScore.value = playerScoreString ? parseInt(playerScoreString) : 0;

  const botScoreString = localStorage.getItem("botScore");
  botScore.value = botScoreString ? parseInt(botScoreString) : 0;
});

const props = defineProps<ThingProps>();
</script>

<template>
  <div class="d-flex gap-1 justify-content-center mt-5 mb-3">
    <ButtonStart @click="startGame" text="Start" />
    <ButtonStart @click="restartGame" text="Reset" />
  </div>
  <div class="d-flex justify-content-between align-items-center">
    <div class="playerBox">
      <SelfScore name="Bot" :score="botScore"/>
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
        <SelfScore :name="playerName" :score="playerScore" />
      </div>
      <RightPlayer :choosedThing="choosedThing || 'paper'"/>
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
