<!-- <script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style> -->
<template>
 <head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"><h1>Wish Simulator</h1></div>
    <button type="button" id="btn" class="btn">Wish</button>
    <button type="button" id="btn2" class="btn">Wish Till Ya Get 5 Star</button>
    <div class="data"> Games Played: <span id="games" class="number">0</span></div>
    <div> Average Pulls per 5 Star: <span id="wish" class="number">-</span></div>
    <div>Last Pity: <span id="last" class="number">0</span></div>
    <div>Wishes Before 5 Star: <span id="pull" class="number">0</span></div>
    <div id="fifty"></div>
    <div>
        <h2>{{ Destination.name }}</h2>
        <h3>{{ clicked }}</h3>
        <button @clicked="increment">Click Me</button>
    </div>
  </body>
</template>

<script setup>
import HomeView from "./views/HomeView.vue"
let i = 0;
let factor = 0.006;
let history = []
const DOMSelectors = {
  button: document.querySelector('#btn'),
  button2: document.querySelector('#btn2'),
  fifty: document.querySelector('#fifty')
};

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