<template>
  <div id="app">
    <img
      alt="Secret Hitler logo"
      src="./assets/logo.png"
      width="10%"
      height="10%"
    />
    <transition name="slide-fade" mode="out-in">
      <div v-if="!newGame && !joinGame && !inGame">
        <div>
          <input v-model="gameCode" /><br />
          <button v-on:click="joinGameLobby">Join Game</button>
        </div>
        OR
        <div>
          <button v-on:click="createNewGame">Create Game</button>
        </div>
      </div>
      <CreateGame v-if="newGame" />
      <GameLobby
        v-if="joinGame"
        v-bind:playerName="playerName"
        v-bind:gameCode="gameCode"
      />
      <GameBoard v-if="inGame" />
    </transition>
  </div>
</template>

<script>
import CreateGame from "./components/CreateGame.vue";
import GameLobby from "./components/GameLobby.vue";
import GameBoard from "./components/GameBoard.vue";
const _ = require('lodash');

export default {
  name: "App",
  data: function () {
    return {
      inGame: false,
      newGame: false,
      joinGame: false,
      playerName: 'Comrade',
      gameCode: '****',
      deck: ['l', 'l', 'l', 'l', 'l', 'l', 'f', 'f', 'f', 'f', 'f', 'f', 'f', 'f', 'f', 'f', 'f'],
      discard: [],
      hand: [],
      liberalBoard: 0,
      fascistBoard: 0,
      winner: '',
      gameOver: false
    };
  },
  components: {
    CreateGame,
    GameLobby,
    GameBoard
  },
  methods: {
    createNewGame: function () {
      this.newGame = true;
      this.joinGame = false;
      this.inGame = false;
    },
    joinGameLobby: function () {
      this.newGame = false;
      this.joinGame = true;
      this.inGame = false;
    },
    startGame: function () {
      this.newGame = false;
      this.joinGame = false;
      this.inGame = true;
      this.deck = _.shuffle(this.deck)
    },
    createGame: function () {
      const randomCode = _.random(9999).toString();
      this.gameCode = randomCode.padStart(4, 0);
      this.joinGameLobby();
    },
    drawTiles: function () {
      this.hand = _.pullAt(this.deck, [0, 1, 2]);
    },
    discardTile: function (idx) {
      let selectedCard = this.hand[idx];
      this.discard.push(selectedCard);
      this.hand.splice(idx, 1);
    },
    playTile: function (idx) {
      let tile = this.hand[idx];
      if(tile === 'l')
        this.liberalBoard += 1;
      else
        this.fascistBoard += 1;
      this.discard.push(this.hand[1 - idx]);
      this.hand.splice(0, 2);

      if(this.deck.length < 3) {
        this.deck = _.shuffle(this.discard);
        this.discard = [];
      }

      if(this.liberalBoard === 6) {
        this.winner = 'Liberals';
        this.gameOver = true;
      } else if (this.fascistBoard === 6) {
        this.winner = 'Fascists';
        this.gameOver = true;
      }
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333333;
  margin-top: 60px;
}

.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>
