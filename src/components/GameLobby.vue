<template>
  <div>
    <h1>Lobby {{ gameCode }} </h1>
    <p>Players</p>
    <ul>
      <li>{{ playerName }}</li>
    </ul>
    <button v-on:click="$parent.startGame">Start Game</button>
  </div>
</template>

<script>
export default {
  name: "GameLobby",
  props: {
    gameCode: String,
    playerName: String
  }
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
</style>
