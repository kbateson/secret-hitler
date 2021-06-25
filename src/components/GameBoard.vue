<template>
  <div id="board">
    <div v-if="$parent.gameOver">Game over! {{ $parent.winner }} win!</div>
    <Deck v-else />
    <div id="liberal-game-space">
      <div
        v-for="n in $parent.liberalBoard"
        v-bind:key="n"
        v-bind:style="calculatePosition(n, true)"
      >
        <img src="../assets/l_tile.png" width="140px" height="200px" />
      </div>

      <div
        style="
          width: 1000px;
          height: 400px;
          position: relative;
          z-index: 1;
          margin-left: auto;
          margin-right: auto;
        "
      >
        <img
          id="liberal-board"
          src="../assets/l_board.png"
          width="1000px"
          height="400px"
        />
      </div>
    </div>

    <div id="fascist-game-space">
      <div id="fascist-board">
        <div
          v-for="n in $parent.fascistBoard"
          v-bind:key="n"
          v-bind:style="calculatePosition(n, false)"
        >
          <img src="../assets/f_tile.png" width="140px" height="200px" />
        </div>

        <div
          style="
            width: 1000px;
            height: 400px;
            position: relative;
            z-index: 1;
            margin-left: auto;
            margin-right: auto;
          "
        >
          <img src="../assets/f_board.png" width="1000px" height="400px" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Deck from "./Deck.vue";

export default {
  name: "GameBoard",
  components: {
    Deck,
  },
  methods: {
    calculatePosition(n, l) {
      let style = `
          width: 130;
          height: 200;
          position: absolute;
          left: ${200 + (l ? 80 : 0) + (n * 140)}px
          top: 420px;
          z-index: ${2};
        `;

      return style;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#liberal-game-space {
  text-align: left;
  position: relative;
  top: 0;
  left: 0;
}
#liberal-board {
  position: relative;
  top: 0;
  left: 0;
}

#fascist-game-space {
  text-align: left;
  position: relative;
  top: 0;
  left: 0;
}
#fascist-board {
  position: relative;
  top: 0;
  left: 0;
}
</style>
