<template>
  <div class="container">
    <h1>Play Tic Tac Toe</h1>
    <GameBoard />
    <h2 id="winner" />
    <button @click="handleReset" class="reset-button">RESET BOARD</button>
  </div>
</template>

<script>
import GameBoard from "./components/GameBoard.vue";
export default {
  name: "App",
  components: { GameBoard },
  data() {
    return {};
  },
  methods: {
    handleReset() {
      window.location.reload();
    },
  },
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

.block:hover {
  cursor: pointer;
  background: #0ff30f;
}
.reset-button {
  margin-top: 20px;
  outline: none;
  border: 4px solid green;
  padding: 10px 20px;
  font-size: 1rem;
  font-weight: bold;
  background: none;
  transition: all 0.2s ease-in-out;
}

.reset-button:hover {
  cursor: pointer;
  background: green;
  color: white;
}
</style>
