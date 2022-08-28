<template>
  <Game msg="Morpion"></Game>
  <Rules v-if="step == 1" @nextstep="nextstep"></Rules>
  <Interface v-if="step == 2" @PlayerList="updatePlayerList" @SymbolList="updateSymbolList" @nextstep="nextstep">
  </Interface>
  <Morpion v-if="step == 3"></Morpion>
  <Win v-if="step == 4"></Win>
</template>
<script>
import Game from './components/Game.vue'
import Rules from './components/Rules.vue'
import Interface from './components/Interface.vue'
import Morpion from './components/Morpion.vue'
import Win from './components/Win.vue'
export default {

  name: 'App',
  data() {
    return {
      step: 1,
      namePlayers: [],
      symbolPlayers: [],
      winner: ''
    }
  },
  methods: {
    nextstep() {
      this.step++
    },
    updatePlayerList(value) {
      this.namePlayers = value;
    },
    updateSymbolList(value) {
      this.symbolPlayers = value;
    }
  },
  components: {
    Game,
    Rules,
    Interface,
    Morpion,
    Win
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  color: black;
  background-color: lightblue;
}

button {
  margin-top: 10px;
  background-color: lightgray;
  border-color: gray;
  border-radius: 5em;
}

button:hover {
  background-color: gray;
  border-color: lightgray;
  color: whitesmoke;
}

@media screen and (max-width: 600px) {
  button {
    margin-top: 5px;
  }
}
</style>
