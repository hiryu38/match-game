<template>
<div id="app">
  <div class="container mt-5">
    <h1>3 Match Game</h1>
    <h2 class="text-right">{{ turnMessage }}</h2>
    <div id="game-board" class="mt-5">
      <div class="row">
        <div class="col-md-4 text-center border" v-for="(field, idx) in fields" :key="idx" @click="setFigure(idx);">
          <div style="height:200px; width:200px; background-color:lightgray;margin-right:auto;margin-left:auto">
            <span class="display-1">{{ field.figure }}</span>
          </div>
          {{ field.xCoordinate }} - {{ field.yCoodinate }}
        </div>
      </div>
    </div>
    <button class="mt-4 btn btn-primary btn-block" @click="resetField();">
      Reset Game
    </button>
  </div>
</div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      player1: {
        figure: "O"
      },
      player2: {
        figure: "X"
      },
      fields: [{
          xCoordinate: 0,
          yCoodinate: 0,
          figure: ""
        },
        {
          xCoordinate: 0,
          yCoodinate: 1,
          figure: ""
        },
        {
          xCoordinate: 0,
          yCoodinate: 2,
          figure: ""
        },
        {
          xCoordinate: 1,
          yCoodinate: 0,
          figure: ""
        },
        {
          xCoordinate: 1,
          yCoodinate: 1,
          figure: ""
        },
        {
          xCoordinate: 1,
          yCoodinate: 2,
          figure: ""
        },
        {
          xCoordinate: 2,
          yCoodinate: 0,
          figure: ""
        },
        {
          xCoordinate: 2,
          yCoodinate: 1,
          figure: ""
        },
        {
          xCoordinate: 2,
          yCoodinate: 2,
          figure: ""
        }
      ],
      player1Turn: true,
      gameOver: false
    };
  },
  methods: {
    setFigure(idx) {
      if (!this.gameOver && this.fields[idx].figure === "") {
        if (this.player1Turn) {
          this.fields[idx].figure = this.player1.figure;
          this.player1Turn = false;
          this.checkGameOver();
        }

      }
    },
    resetField() {
      for (var i = 0; i < this.fields.length; i++) {
        this.fields[i].figure = "";
      }
      this.player1Turn = true;
      this.gameOver = false;
    },
    cpuTurn() {
      var idx = -1;
      var result = -1;
      for (var i = 0; i < this.fields.length; i++) {
        if (result < this.checkField(i)) {
          idx = i;
          break;
        }
      }
      console.log(idx);
      this.fields[idx].figure = this.player2.figure;
    },
    checkField(idx) {
      if (this.fields[idx].figure !== "") {
        return -1;
      } else {
        return 4;
      }
    },
    checkGameOver() {
      // 0, 1, 2
      // 0, 4, 8
      // 0, 3, 6
      // 1, 4, 7
      // 2, 4, 6
      // 2, 5, 8
      // 3, 4, 5
      // 6, 7, 8
      if (this.fields[0].figure !== "" && this.fields[1].figure !== "" && this.fields[2].figure !== "") {
        if (this.fields[0].figure == this.fields[1].figure && this.fields[1].figure == this.fields[2].figure) {
          this.gameOver = true;
        }
      }
      if (this.fields[0].figure !== "" && this.fields[4].figure !== "" && this.fields[8].figure !== "") {
        if (this.fields[0].figure == this.fields[4].figure && this.fields[4].figure == this.fields[8].figure) {
          this.gameOver = true;
        }
      }
      if (this.fields[0].figure !== "" && this.fields[3].figure !== "" && this.fields[6].figure !== "") {
        if (this.fields[0].figure == this.fields[3].figure && this.fields[3].figure == this.fields[6].figure) {
          this.gameOver = true;
        }
      }
      if (this.fields[1].figure !== "" && this.fields[4].figure !== "" && this.fields[7].figure !== "") {
        if (this.fields[1].figure == this.fields[4].figure && this.fields[4].figure == this.fields[7].figure) {
          this.gameOver = true;
        }
      }
      if (this.fields[2].figure !== "" && this.fields[4].figure !== "" && this.fields[6].figure !== "") {
        if (this.fields[2].figure == this.fields[4].figure && this.fields[4].figure == this.fields[6].figure) {
          this.gameOver = true;
        }
      }
      if (this.fields[2].figure !== "" && this.fields[5].figure !== "" && this.fields[8].figure !== "") {
        if (this.fields[2].figure == this.fields[5].figure && this.fields[5].figure == this.fields[8].figure) {
          this.gameOver = true;
        }
      }
      if (this.fields[3].figure !== "" && this.fields[4].figure !== "" && this.fields[5].figure !== "") {
        if (this.fields[3].figure == this.fields[4].figure && this.fields[4].figure == this.fields[5].figure) {
          this.gameOver = true;
        }
      }
      if (this.fields[6].figure !== "" && this.fields[7].figure !== "" && this.fields[8].figure !== "") {
        if (this.fields[6].figure == this.fields[7].figure && this.fields[7].figure == this.fields[8].figure) {
          this.gameOver = true;
        }
      }
    }
  },
  computed: {
    turnMessage() {
      if (!this.gameOver) {
        if (this.player1Turn) {
          return "Player 1 turn";
        } else {
          return "Player 2 turn";
        }
      } else {
        return "Game Over";
      }
    }
  },
  watch: {
    player1Turn(value) {
      if (!this.gameOver && !value) {
        this.cpuTurn();
        this.player1Turn = true;
        this.checkGameOver();
      }
    }
  }
};
</script>

<style></style>
