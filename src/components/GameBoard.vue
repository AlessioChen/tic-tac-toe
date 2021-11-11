<template>
  <div class="play-area">
    <div
      v-for="(item, index) in board"
      :key="index"
      :id="'block_' + index"
      class="block"
      :class="{ red: winCoords.includes(index) }"
      ref="name"
      @click="handleClick(index)"
    >
      {{ board[index] }}
    </div>
  </div>

  <button @click="handleReset" class="reset-button">RESET BOARD</button>
  <h1 v-if="winner">The winner is '{{ winner }}'</h1>
  <h1 v-else-if="draw">It's a draw game</h1>
</template>

<script>
import { computed, reactive, ref } from "@vue/reactivity";
export default {
  name: "GameBoard",

  setup() {
    //variable
    let currentPlayer = "x";
    let board = reactive(["", "", "", "", "", "", "", "", ""]);
    let winCoords = ref([]);
    let draw = ref(false);
    let moves = 0;

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

    //Cell click
    const handleClick = (blockId) => {
      if (winner.value) {
        moves = 0;
        draw.value = false;
        return;
      }
      if (moves == 8) {
        draw.value = true;
        moves = 0;
      }
      if (board[blockId] == "") {
        board[blockId] = currentPlayer;
        currentPlayer = currentPlayer === "o" ? "x" : "o";
        moves++;
      }
    };

    //Reset game
    const handleReset = () => {
      winCoords.value = [];
      draw.value = false;
      moves = 0;
      for (let i = 0; i < board.length; i++) board[i] = "";
    };

    //Check game win
    const checkWin = () => {
      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          winCoords.value = lines[i];
          return board[a];
        }
      }

      return null;
    };

    return { handleClick, board, winner, handleReset, winCoords, draw };
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

.red {
  background: red;
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