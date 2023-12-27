<script setup lang="ts">
import { ref } from 'vue'


const tics = ref({
    aA: '',
    aB: '',
    aC: '',
    bA: '',
    bB: '',
    bC: '',
    cA: '',
    cB: '',
    cC: '',
});

const player = ref("One");
const gameOver = ref('');

const handleReset = ()=>{
    tics.value = {
    aA: '',
    aB: '',
    aC: '',
    bA: '',
    bB: '',
    bC: '',
    cA: '',
    cB: '',
    cC: '',
};
player.value = "One";
gameOver.value = '';
}

const checkStatus = ()=>{
    const checkAllEmpties = Object.entries(tics.value).flatMap((entry) => entry[1]).filter(entry => entry === '');
    if(checkAllEmpties.length === 0) gameOver.value = "No Winner" ;

    if(tics.value.aA && tics.value.aA === tics.value.aB && tics.value.aA === tics.value.aC) gameOver.value = player.value;
    if(tics.value.bA && tics.value.bA === tics.value.bB && tics.value.bA === tics.value.bC) gameOver.value = player.value;
    if(tics.value.cA && tics.value.cA === tics.value.cB && tics.value.cA === tics.value.cC) gameOver.value = player.value;
    if(tics.value.aA && tics.value.aA === tics.value.bA && tics.value.aA === tics.value.cA) gameOver.value = player.value;
    if(tics.value.aB && tics.value.aB === tics.value.bB && tics.value.aB === tics.value.cB) gameOver.value = player.value;
    if(tics.value.aC && tics.value.aC === tics.value.bC && tics.value.aC === tics.value.cC) gameOver.value = player.value;
    if(tics.value.aA && tics.value.aA === tics.value.bB && tics.value.aA === tics.value.cC) gameOver.value = player.value;
    if(tics.value.cA && tics.value.cA === tics.value.bB && tics.value.cA === tics.value.aC) gameOver.value = player.value;
}

const handleClick = (key: 'aA' | 'aB' | 'aC' | 'bA' | 'bB' | 'bC' | 'cA' |'cB' |'cC') =>{
    if(gameOver.value) return
    if(tics.value[key] !== '') return
    tics.value[key] = player.value;
    checkStatus()
    if(gameOver.value) return
    player.value = player.value === 'One'? "Two" : 'One';

}

const handleMessage = ()=> {
    if(gameOver.value === 'No Winner') return "All tics are tacked, but no winner!"
    if(gameOver.value === 'One' || gameOver.value === 'Two') return `Player ${player.value} wins!`
    return `It is player ${player.value === 'One'? 'X' : 'O'}'s turn.'`
}


</script>

<template>

<link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">

<div class="container py-5" style="height: 100vh;">
        <div class="row">
            <div class="col-md-4">
                <div class="card mt-3" style="width: 18rem;">
                    <a href="javascript: void(0)" class="text-decoration-none">
                        <div class="card-body">
                            <h5 class="card-title">Tic Tac Toe Game</h5>
                            <p class="card-text">A CSS layout module.</p>
                        </div>
                    </a>
                </div>
            </div>
<div class="w3-container">
  <h2>Tic Tac Toe Game</h2>
  
  <button onclick="document.getElementById('id01').style.display='block'" class="w3-button w3-black">Start</button>

  <div id="id01" class="w3-modal">
    <div class="w3-modal-content">
      <header class="w3-container w3-teal"> 
        <span onclick="document.getElementById('id01').style.display='none'" 
        class="w3-button w3-display-topright">&times;</span>
      </header>
      <div class="w3-container">
        <h2>{{handleMessage()}}</h2>
   <button v-if="gameOver !== ''" @click="handleReset()">Reset?</button>

   <div class="tile-container">
        <div v-for="value,key in tics" @click="handleClick(key)" class="tiles">
            {{value === 'One'? 'X': value === 'Two'? 'O': ''}}
        </div>
   </div>
      </div>
      
        
      
    </div>
  </div>
</div>
   </div>
</div>

</template>

<style>
:root {
    font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
    font-size: 16px;
    line-height: 24px;
    font-weight: 400;
  
    color-scheme: light dark;
    color: rgba(255, 255, 255, 0.87);
    background-color: #242424;
  
    font-synthesis: none;
    text-rendering: optimizeLegibility;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    -webkit-text-size-adjust: 100%;
  }
  
  a {
    font-weight: 500;
    color: #646cff;
    text-decoration: inherit;
  }
  a:hover {
    color: #535bf2;
  }
  
  
  
  h1 {
    font-size: 3.2em;
    line-height: 1.1;
  }
  
  button {
    border-radius: 8px;
    border: 1px solid transparent;
    padding: 0.6em 1.2em;
    font-size: 1em;
    font-weight: 500;
    font-family: inherit;
    background-color: #1a1a1a;
    cursor: pointer;
    transition: border-color 0.25s;
  }
  button:hover {
    border-color: #646cff;
  }
  button:focus,
  button:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
  }
  
  .card {
    padding: 2em;
  }
  
  #app {
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;
    text-align: center;
  }
  
  .tile-container{
    margin: auto;
    display: grid;
    grid-template-columns: auto auto auto;
    padding: 2em;
    margin: 2em;
  }
  .tiles{
    width: 60px;
    height: 30px;
    background-color: #fff;
    color: #242424;
    padding: 1em;
    border: 2px solid #242424;
  }
  
  @media (prefers-color-scheme: light) {
    :root {
      color: #213547;
      background-color: #ffffff;
    }
    a:hover {
      color: #747bff;
    }
    button {
      background-color: #f9f9f9;
    }
  }
  
</style>
