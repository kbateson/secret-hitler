<template>
<div>
    <div id="discard">
      Discard<br />
      Count: {{ $parent.$parent.discard.length }}<br />
    </div>
  <div id="deck">
      Deck<br />
      Count: {{ $parent.$parent.deck.length }}<br />
      <button v-on:click="$parent.$parent.drawTiles" v-if="$parent.$parent.hand.length === 0">Draw</button>
  </div>
  <div v-if="$parent.$parent.hand.length === 3">
      <span v-for="(tile, idx) in $parent.$parent.hand" v-bind:key="idx">
        <img src="@/assets/l_tile.png" v-if="tile === 'l'" v-on:click="$parent.$parent.discardTile(idx)" />
        <img src="@/assets/f_tile.png" v-else-if="tile === 'f'" v-on:click="$parent.$parent.discardTile(idx)" />
      </span>
  </div>
  <div v-if="$parent.$parent.hand.length === 2">
      <span v-for="(tile, idx) in $parent.$parent.hand" v-bind:key="idx">
        <img src="@/assets/l_tile.png" v-if="tile === 'l'" v-on:click="$parent.$parent.playTile(idx)" />
        <img src="@/assets/f_tile.png" v-else-if="tile === 'f'" v-on:click="$parent.$parent.playTile(idx)" />
      </span>
  </div>
  </div>
</template>

<script>
export default {
  name: "Deck",
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
