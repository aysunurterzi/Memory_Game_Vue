<template>
  <div id="app">
    <div class="main-container">
      <h1 class="game-title">🧠 Memory Game</h1>
      <button @click="startGame" v-if="!gameStarted" class="start-button">
        <span>🎮 START GAME</span>
      </button>
      <GameBoard v-if="gameStarted" />
    </div>
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue';

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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#app {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.main-container {
  text-align: center;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  padding: 40px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.game-title {
  font-size: 3rem;
  color: white;
  margin-bottom: 30px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  font-weight: 700;
}

.start-button {
  background: linear-gradient(45deg, #ff6b6b, #ee5a52);
  border: none;
  border-radius: 50px;
  padding: 20px 40px;
  font-size: 1.5rem;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(238, 90, 82, 0.4);
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.start-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(238, 90, 82, 0.6);
  background: linear-gradient(45deg, #ee5a52, #ff6b6b);
}

.start-button:active {
  transform: translateY(-1px);
}

.start-button span {
  display: inline-block;
  transition: transform 0.3s ease;
}

.start-button:hover span {
  transform: scale(1.05);
}
</style>
