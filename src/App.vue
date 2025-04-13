<script setup>
import GameBoard from './components/GameBoard.vue'
import TicTacToeIcon from './components/icons/TTTIcon.vue'
</script>

<template>
  
  <div class="gameboard">
    <TicTacToeIcon class="ttticon"/>
    <div class="heading">
      
      <h1>The Tic Tac Toe Game    </h1>
  </div>
    <GameBoard/>
  </div>
</template>

<style>
body {
    background-color: rgb(48, 33, 33)  
    
}
.heading {

}
.gameboard {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    
    
  }
  .ttticon{
    fill: var(--color-text);
  }
  
</style>