
<template>
  <div id="content">
    <div id="content__heading">
      <h1>Wish Simulator</h1>
    </div>
    <button class="content__button content__wish-button" @click="performClick">Wish</button>
    <button class="content__button" @click="doWishUntilWin">Wish Till Ya Get 5 Star</button>
    <div class="content__data"> Games Played: <span id="games" class="content__number">{{ history.length }}</span></div>
    <div> Average Pulls per 5 Star: <span id="wish" class="content__number">{{ getAverage() }}</span></div>
    <div>Last Pity: <span id="last" class="content__number">{{ lastPity }}</span></div>
    <div>Wishes Before 5 Star: <span id="pull" class="content__number">{{ pullCount }}</span></div>
    <div v-bind:style="{ color: statusColor }"><strong>{{ fiftyStatus }}</strong></div>
    <p>Last {{ historyDisplayCount() }} games:</p>
    <div v-for="i in historyDisplayCount()">{{ history[history.length - i] }}</div>
  </div>
</template>
<script setup>
import { ref } from 'vue'
const fiftyStatus = ref('')
const pullCount = ref('0')
let i = 0;
let factor = 0.006;
let lastPity = 0;
let history = []
let statusColor = "black";
let historyDisplayCount = () => {
  return Math.min(history.length, 3)
}
function doWishUntilWin() {
  performClick();
  while (i > 0) {
    performClick();
  }
}
function performClick() {
  if (i >= 73) {
    factor = Math.min(1, factor + 0.06)
  }
  if (getRandomNumber()) {
    return
  }
  i++;
  console.log(i);
  console.log(factor);
  // document.getElementById("pull").innerText = i
  pullCount.value = i
}
function getRandomNumber() {
  const a = Math.floor(Math.random() * 1000);
  if (a < (factor * 1000)) {
    obtainWin();
    return true
  }
  console.log(a)
  return false
}
let f = 1
function playFiftyFifty() {
  fiftyStatus.value = ""
  statusColor = "black";
  const a = Math.random();
  if (f % 2 === 0) {
    console.log("Guaranteed")
    fiftyStatus.value = "Guaranteed Win"
    f++;
    return
  }
  if (a < 0.5) {
    statusColor = "red";
    f++;
    console.log("You lost the 50-50")
    fiftyStatus.value = "You lost the 50-50! D:"
    return
  }
  console.log("You won the 50-50")
  fiftyStatus.value = "You won the 50-50! :D"
}
function obtainWin() {
  playFiftyFifty();
  let turns = i + 1
  console.log("Nice! You got a 5 star after " + (turns) + " pulls")
  history.push(turns)
  factor = 0.006
  lastPity = turns;
  i = 0
}
function getAverage() {
  if (history.length == 0) {
    return "-"
  }
  let sum = 0
  for (let x of history) {
    sum = sum + x
  }
  return Math.round(sum / history.length * 100) / 100
}
</script>

<style scoped>
#app {
  align-items: center;
}

#content {
  align-items: center;
  text-align: center;
}

.content__data {
  margin-top: 1rem;
}

.content__button {
  height: 2rem;
  background: black;
  color: rgb(192, 110, 255)
}

.content__number {
  font-weight: bold;
  color: rgb(0, 110, 255);
}

.content__wish-button {
  margin-inline-end: 0.5rem;
}</style>