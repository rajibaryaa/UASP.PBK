<template>
  <div class="tic-tac-toe-widget">
    <h2>Tic Tac Toe</h2>
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" @click="handleClick(index)">{{ cell }}</div>
    </div>
    <button @click="resetGame">Reset</button>
    <p>{{ status }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: ['', '', '', '', '', '', '', '', ''],
      currentPlayer: 'X',
      isGameEnded: false,
    };
  },
  computed: {
    status() {
      if (this.isGameEnded) {
        return 'Game Over!';
      }
      return `Player ${this.currentPlayer}'s turn`;
    },
  },
  methods: {
    handleClick(index) {
      if (!this.isGameEnded && this.board[index] === '') {
        this.board[index] = this.currentPlayer;
        this.checkWinner();
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
      }
    },
    checkWinner() {
      const winningCombinations = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
        [0, 4, 8], [2, 4, 6], // Diagonals
      ];

      for (const combination of winningCombinations) {
        const [a, b, c] = combination;
        if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
          this.isGameEnded = true;
          return;
        }
      }
    },
    resetGame() {
      this.board = ['', '', '', '', '', '', '', '', ''];
      this.currentPlayer = 'X';
      this.isGameEnded = false;
    },
  },
};
</script>

<style scoped>
.tic-tac-toe-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  margin-bottom: 10px;
}

.board div {
  border: 1px solid black;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

button {
  margin-top: 10px;
}
</style>
