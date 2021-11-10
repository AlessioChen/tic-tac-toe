<template>
  <div :board="board" @reset="reset" class="play-area">
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
</template>

<script>
export default {
  name: "GameBoard",
  data() {
    return {
      currenPlayer: "x",
      moves: 0,
      board: [],
    };
  },

  methods: {
    reset() {
      console.log("reset");
    },
    handleClick(blockId) {
      if (this.board[blockId] == null && this.moves < 9) {
        if (this.currenPlayer == "x") {
          this.board[blockId] = "x";
          this.currenPlayer = "o";
        } else {
          this.board[blockId] = "o";
          this.currenPlayer = "x";
        }
        this.move++;
      }
    },
  },
};
</script>

<style>
.play-area {
  margin-top: 10px;
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