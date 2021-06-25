<template>
  <div>
    <h1>Let's make a game.</h1>
    <p>What should we call you?</p>
    <p>
      <input v-model="$parent.playerName" />
    </p>
    <p>
      <button v-on:click="$parent.createGame">Create Game</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "CreateGame"
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
