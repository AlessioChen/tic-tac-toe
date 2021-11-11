<template>
  <div :board="board" class="play-area">
    <div id="block_0" @click="handleClick(0)" class="block">{{ board[0] }}</div>
    <div id="block_1" @click="handleClick(1)" class="block">{{ board[1] }}</div>
    <div id="block_2" @click="handleClick(2)" class="block">{{ board[2] }}</div>
    <div id="block_3" @click="handleClick(3)" class="block">{{ board[3] }}</div>
    <div id="block_4" @click="handleClick(4)" class="block">{{ board[4] }}</div>
    <div id="block_5" @click="handleClick(5)" class="block">{{ board[5] }}</div>
    <div id="block_6" @click="handleClick(6)" class="block">{{ board[6] }}</div>
    <div id="block_7" @click="handleClick(7)" class="block">{{ board[7] }}</div>
    <div id="block_8" @click="handleClick(8)" class="block">{{ board[8] }}</div>
  </div>
  <button @click="handleReset" class="reset-button">RESET BOARD</button>
  <h2 v-if="winner">{{ winner }}</h2>
</template>

<script>
import { computed, reactive, ref } from "@vue/reactivity";
export default {
  name: "GameBoard",

  setup() {
    let currentPlayer = "x";
    let moves = 0;
    let board = reactive(["", "", "", "", "", "", "", "", ""]);

    const winner = computed(() => checkWin());

    const lines = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6],
    ];

    const handleClick = (blockId) => {
      if (winner.value) return;

      board[blockId] = currentPlayer;
      currentPlayer = currentPlayer === "o" ? "x" : "o";
    };

    const handleReset = () => {
      for (let i = 0; i < board.length; i++) board[i] = "";
    };
    const checkWin = () => {
      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          return board[a];
        }
      }

      return null;
    };

    return { handleClick, board, winner, handleReset };
  },
};
</script>

<style>
.play-area {
  margin-top: 20px;
  display: grid;
  width: 300px;
  height: 300px;
  grid-template-columns: auto auto auto;
}
.block {
  display: flex;
  width: 100px;
  height: 100px;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
  font-weight: bold;
  border: 3px solid black;
  transition: background 0.2s ease-in-out;
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

/* Top border */
#block_0,
#block_1,
#block_2 {
  border-top: none;
}

/* Left border */
#block_0,
#block_3,
#block_6 {
  border-left: none;
}

/* Botton border */

#block_6,
#block_7,
#block_8 {
  border-bottom: none;
}

/* right border */
#block_2,
#block_5,
#block_8 {
  border-right: none;
}
</style>