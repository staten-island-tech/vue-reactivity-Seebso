<template>
    <div>
        <h3>{{ clicked }}</h3>
        <button @clicked="increment">Wish</button>
    </div>
</template>

<script setup>
function increment(){
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

<style lang="scss" scoped>

</style>
