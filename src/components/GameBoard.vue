<template>
  <div class="game-board">
    <div class="control-panel">
      <button @click="startGame">Başla</button>
      <button @click="pauseGame">{{ isPaused ? 'Devam' : 'Durdur' }}</button>
      <div class="timer">{{ formatTime }}</div>
    </div>
    <div class="cards-grid">
      <MemoryCard
        v-for="(card, index) in cards"
        :key="card.id"
        :color="card.isFlipped || card.isMatched ? card.color : 'grey'"
        :is-flipped="card.isFlipped"
        :is-matched="card.isMatched"
        @click="handleCardClick(index)"
      />
    </div>
  </div>
</template>

<script>
import MemoryCard from './MemoryCard.vue';

export default {
  name: 'GameBoard',
  components: {
    MemoryCard
  },
  data() {
    return {
      colors: [
        'red', 'blue', 'pink', 'green',
        'yellow', 'orange', 'black', 'purple'
      ],
      cards: [],
      flippedCards: [],
      disableClicks: false,
      startTime: 0,
      currentTime: 0,
      totalTime: 60, // 1 dakika (60 saniye)
      timerInterval: null,
      isPaused: false
    };
  },
  computed: {
    formatTime() {
      const minutes = Math.floor(this.currentTime / 60);
      const seconds = this.currentTime % 60;
      return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    }
  },
  created() {
    this.initializeGame();
  },
  unmounted() {
    clearInterval(this.timerInterval);
  },
  methods: {
    initializeGame() {
      this.cards = this.getShuffledColors().map((color, index) => ({
        id: index,
        color,
        isFlipped: false,
        isMatched: false
      }));
      this.flippedCards = [];
      this.disableClicks = false;
      this.currentTime = 0;
      this.isPaused = false;
      clearInterval(this.timerInterval);
    },
    startTimer() {
      this.startTime = Math.floor(Date.now() / 1000);
      this.timerInterval = setInterval(() => {
        if (!this.isPaused) {
          this.currentTime = Math.floor(Date.now() / 1000) - this.startTime;
          if (this.currentTime >= this.totalTime) {
            clearInterval(this.timerInterval);
            // Oyun süresi dolduğunda yapılacak işlemler buraya eklenebilir
          }
        }
      }, 1000);
    },
    startGame() {
      this.initializeGame();
      this.startTimer();
    },
    pauseGame() {
      if (this.isPaused) {
        this.resumeGame();
      } else {
        this.isPaused = true;
        this.disableClicks = true;
      }
    },
    resumeGame() {
      this.isPaused = false;
      this.disableClicks = false;
      this.startTime = Math.floor(Date.now() / 1000) - this.currentTime;
    },
    handleCardClick(index) {
      if (this.disableClicks || this.isPaused) return;

      const card = this.cards[index];
      if (card.isMatched || card.isFlipped || this.flippedCards.length === 2) {
        return;
      }
      card.isFlipped = true;
      this.flippedCards.push(index);
      if (this.flippedCards.length === 2) {
        this.checkMatch();
      }
    },
    checkMatch() {
      this.disableClicks = true;
      const [firstIndex, secondIndex] = this.flippedCards;
      const firstCard = this.cards[firstIndex];
      const secondCard = this.cards[secondIndex];
      if (firstCard.color === secondCard.color) {
        firstCard.isMatched = true;
        secondCard.isMatched = true;
        this.resetFlippedCards();
        this.checkAllMatched();
      } else {
        setTimeout(() => {
          firstCard.isFlipped = false;
          secondCard.isFlipped = false;
          this.resetFlippedCards();
        }, 1000);
      }
    },
    resetFlippedCards() {
      this.flippedCards = [];
      this.disableClicks = false;
    },
    checkAllMatched() {
      const allMatched = this.cards.every(card => card.isMatched);
      if (allMatched) {
        clearInterval(this.timerInterval);
      }
    },
    getShuffledColors() {
      return this.colors
        .concat(this.colors) // Her rengi iki kez ekleyerek eşleşmeleri sağlayın
        .sort(() => Math.random() - 0.5); // Renkleri karıştır
    }
  }
}
</script>

<style scoped>
.game-board {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.control-panel {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.control-panel button {
  margin-right: 20px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

.timer {
  font-size: 24px;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}
</style>
