<template>
  <div id="app">
    <button @click="startGame" v-if="!gameStarted">Başla</button>
    <GameBoard v-if="gameStarted" />
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue'

export default {
  name: 'App',
  components: {
    GameBoard
  },
  data() {
    return {
      gameStarted: false
    }
  },
  methods: {
    startGame() {
      this.gameStarted = true;
    }
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
  margin-top: 60px;
}
button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>
