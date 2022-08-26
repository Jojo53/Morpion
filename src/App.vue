<template>
  <Game msg="Morpion"></Game>
  <Rules v-if="step == 1" @nextstep="nextstep"></Rules>
  <Interface v-if="step == 2" @PlayerList="updatePlayerList" @SymbolList="updateSymbolList" @nextstep="nextstep">
  </Interface>
  <Morpion v-if="step == 3"></Morpion>
</template>
<script>
import Game from './components/Game.vue'
import Rules from './components/Rules.vue'
import Interface from './components/Interface.vue'
import Morpion from './components/Morpion.vue'
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
    Morpion
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

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
