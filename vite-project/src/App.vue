
<template>
 <head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"><h1>Wish Simulator</h1></div>
    <button @click="oneclick">Wish</button>
    <button @click="wishes">Wish Till Ya Get 5 Star</button>
    <div class="data"> Games Played: <span id="games" class="number">0</span></div>
    <div> Average Pulls per 5 Star: <span id="wish" class="number">-</span></div>
    <div>Last Pity: <span id="last" class="number">0</span></div>
    <div>Wishes Before 5 Star:  <span id="pull" class="number">0</span></div>
    <div id="fifty">{{ five }}</div>  
    <p v-for="i in 3">{{ array[i-1] }}</p>
    

  </body>
</template>

<script setup>
import { ref } from 'vue'
let array = ["Coded by Alvis","I'm so cool","(not)"]
const five = ref('')
let i = 0;
let factor = 0.006;
let history = []
/* const DOMSelectors = {
  button: document.querySelector('#btn'),
  button2: document.querySelector('#btn2'),
  fifty: document.querySelector('#fifty')
}; */
function wishes() {
  oneclick();
  while (i > 0){
    oneclick(); 
  }}
function oneclick(){
    if (i >= 74){
    factor = Math.min(1, factor + 0.06) 
  }
  if (random5()){
    return
  }
  i++;
  console.log(i);
  console.log(factor);
  document.getElementById("pull").innerText = i;
}
function random5() {
  const a = Math.floor(Math.random() * 1000); 
  if (a < (factor * 1000)){ 
    win();
    return true 
  }
  console.log(a)
  return false
}
let f = 1
function fifty() {
  five.value = ""
  const a = Math.random();
  if (f % 2 === 0){
    console.log("Guaranteed")
    five.value = "Guaranteed Win"
    f++;
    return
  }
  if (a < 0.5){
    f++;
    console.log("You lost the 50-50")
    five.value = "You lost the 50-50! D:"
    return
  }
  console.log("You won the 50-50")
  five.value = "You won the 50-50! :D"
}
function win() {
  fifty();
  let turns = i+1
  console.log("Nice! You got a 5 star after " + (turns) + " pulls")
  history.push(turns)
  factor = 0.006
  document.getElementById("games").innerText = history.length;
  document.getElementById("wish").innerText = avg();
  document.getElementById("last").innerText = turns;
  i = 0
}
function avg(){
  let sum = 0
  for (let x of history){ 
    sum = sum + x 
  }
  return Math.round(sum / history.length * 100) / 100 
}
</script>

<style scoped>
#app {
  align-items: center;
}
body {
  align-items: center;
  text-align: center;
}
.data {
  margin-top: 1rem;
}
.btn {
  height: 2rem;
  background: black;
  color: rgb(192, 110, 255)
}
.number {
  font-weight: bold;
  color:rgb(0, 110, 255);
}
</style>