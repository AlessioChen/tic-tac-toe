<template>
  <div class="container">
    <h1>Play Tic Tac Toe</h1>
    <GameBoard />
  </div>
</template>

<script>
import GameBoard from "./components/GameBoard.vue";
export default {
  name: "App",
  components: { GameBoard },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: #eee;
}


</style>
