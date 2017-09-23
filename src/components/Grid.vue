<template lang="html">
  <div>
    <div class="gameStatus" :class="gameStatusColor">
      {{ gameStatusMessage }}
    </div>
    <table class="grid">
      <tr>
        <cell name="1"></cell>
        <cell name="2"></cell>
        <cell name="3"></cell>
      </tr>
      <tr>
        <cell name="4"></cell>
        <cell name="5"></cell>
        <cell name="6"></cell>
      </tr>
      <tr>
        <cell name="7"></cell>
        <cell name="8"></cell>
        <cell name="9"></cell>
      </tr>
    </table>
  </div>
</template>

<script>
import Cell from './Cell.vue';
export default {
  components: { Cell },
  data() {
    return {
      activePlayer: 'O',
      gameStatus: 'turn',
      gameStatusMessage: `O's turn`,
      gameStatusColor: 'statusTurn',
      moves: 0,
      cells: {
        1: '',
        2: '',
        3: '',
        4: '',
        5: '',
        6: '',
        7: '',
        8: '',
        9: ''
      },
      winConditions: [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9], //rows
        [1, 4, 7],
        [2, 5, 8],
        [3, 6, 9], //columns
        [1, 5, 9],
        [3, 5, 7] //diagonals
      ]
    };
  },
  computed: {
    nonActivePlayer() {
      if (this.activePlayer === 'O') {
        return 'X';
      }
      return 'O';
    }
  },
  watch: {
    gameStatus() {
      if (this.gameStatus === 'win') {
        this.gameStatusColor = 'statusWin';
        this.gameStatusMessage = `${this.activePlayer} wins!`;
        Event.$emit('win', this.activePlayer)
        Event.$emit('freeze')
        return;
      } else if (this.gameStatus === 'draw') {
        this.gameStatusColor = 'statusDraw';
        this.gameStatusMessage = 'Draw!';
        return;
      }
    }
  },
  methods: {
    changePlayer() {
      this.activePlayer = this.nonActivePlayer;
    },
    checkForWin() {
      for (var i = 0; i < this.winConditions.length; i++) {
        var wc = this.winConditions[i];
        var cells = this.cells;
        if (this.areEqual(cells[wc[0]], cells[wc[1]], cells[wc[2]])) {
          return true;
        }
      }
      return false;
    },
    areEqual() {
      var len = arguments.length;
      for (var i = 1; i < len; i++) {
        if (arguments[i] === '' || arguments[i] !== arguments[i - 1]) {
          return false;
        }
      }
      return true;
    },
    changeGameStatus() {
      if (this.checkForWin()) {
        return 'win';
      } else if (this.moves === 9) {
        return 'draw';
      }
      this.gameStatusMessage = `${this.nonActivePlayer}'s turn`;

      return 'turn';
    }
  },
  created() {
    Event.$on('strike', cellNumber => {
      this.cells[cellNumber] = this.activePlayer;
      this.moves++;
      this.gameStatus = this.changeGameStatus();
      this.changePlayer();
    });
  }
};
</script>

<style lang="css">
.grid {
	background-color: #34495e;
	color: #fff;
  width: 100%;
  border-collapse: collapse;
}
.gameStatus {
	margin: 0px;
	padding: 15px;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
  background-color: #f1c40f;
  color: #fff;
  font-size: 1.4em;
  font-weight: bold;
}
.statusTurn {
	background-color: #f1c40f;
}
.statusWin {
	background-color: #2ecc71;
}
.statusDraw {
	background-color: #9b59b6;
}
</style>
