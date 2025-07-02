<template>
  <div class="game-board">
    <div class="control-panel">
      <button
        @click="startOrResetGame"
        :class="['control-btn', isGameStarted ? 'reset-btn' : 'start-btn']">
        {{ isGameStarted ? '🔄 Reset' : '▶️ Start' }}
      </button>
      <button 
        @click="pauseGame" 
        :class="['control-btn', 'pause-btn']"
        :disabled="!isGameStarted || isGameWon || isEnd">
        {{ isPaused ? '▶️ Resume' : '⏸️ Pause' }}
      </button>
      <div class="timer">⏰ {{ formatTime }}</div>
    </div>
    <div class="cards-grid">
      <MemoryCard
        v-for="(card, index) in cards"
        :key="card.id"
        :image="card.isFlipped || card.isMatched ? card.image : null"
        :is-flipped="card.isFlipped"
        :is-matched="card.isMatched"
        @click="handleCardClick(index)"
        :disable-click="!isGameStarted || isPaused"
      />
    </div>
    <div v-if="isGameWon" class="modal-overlay" @click="closeModal">
      <div class="modal" @click.stop>
        <div class="modal-content">
          <div class="success-icon">🎉</div>
          <h2>Congratulations!</h2>
          <p>You have successfully completed the game!</p>
          <div class="time-display">
            <span class="time-label">Your Time:</span>
            <span class="time-value">{{ formatTime }}</span>
          </div>
          <button @click="closeModal" class="close-btn">🏠 Main Menu</button>
        </div>
      </div>
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
      animals: [
        'lion', 'elephant', 'cat', 'dog',
        'duck', 'rabbit', 'crocodile', 'giraffe'
      ],
      cards: [],
      flippedCards: [],
      disableClicks: false,
      startTime: 0,
      currentTime: 0,
      totalTime: 60,
      timerInterval: null,
      isPaused: false,
      isGameStarted: false,
      isGameWon: false
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
      this.cards = this.getShuffledAnimals().map((animal, index) => ({
        id: index,
        image: animal,
        isFlipped: false,
        isMatched: false
      }));
      this.flippedCards = [];
      this.disableClicks = false;
      this.currentTime = 0;
      this.isPaused = false;
      this.isGameWon = false;
      clearInterval(this.timerInterval);
    },
    startTimer() {
      this.startTime = Math.floor(Date.now() / 1000);
      this.timerInterval = setInterval(() => {
        if (!this.isPaused) {
          this.currentTime = Math.floor(Date.now() / 1000) - this.startTime;
          if (this.currentTime >= this.totalTime) {
            clearInterval(this.timerInterval);
          }
        }
      }, 1000);
    },
    startOrResetGame() {
      if (this.isGameStarted) {
        this.initializeGame();
      } else {
        this.startGame();
      }
      this.isGameStarted = !this.isGameStarted;

      if (!this.isGameStarted) {
        this.cards = this.getShuffledAnimals().map((animal, index) => ({
          id: index,
          image: animal,
          isFlipped: false,
          isMatched: false
        }));
      }
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
      if (this.disableClicks || this.isPaused || !this.isGameStarted) return;

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
      if (firstCard.image === secondCard.image) {
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
        this.isGameWon = true;
      }
    },
    getShuffledAnimals() {
      return this.animals
        .concat(this.animals)
        .sort(() => Math.random() - 0.5);
    },
    closeModal() {
      this.isGameWon = false;
      this.isEnd = true;
    }
  }
}
</script>

<style scoped>
.game-board {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 600px;
  margin: 0 auto;
}

.control-panel {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
  background: rgba(255, 255, 255, 0.1);
  padding: 20px;
  border-radius: 15px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.control-btn {
  padding: 12px 24px;
  font-size: 16px;
  font-weight: bold;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.start-btn {
  background: linear-gradient(45deg, #4CAF50, #45a049);
  color: white;
}

.reset-btn {
  background: linear-gradient(45deg, #f44336, #da190b);
  color: white;
}

.pause-btn {
  background: linear-gradient(45deg, #ff9800, #f57c00);
  color: white;
}

.pause-btn:disabled {
  background: #cccccc;
  cursor: not-allowed;
  opacity: 0.6;
}

.control-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.timer {
  font-size: 24px;
  font-weight: bold;
  color: white;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  background: linear-gradient(45deg, #2196F3, #1976D2);
  padding: 10px 20px;
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(33, 150, 243, 0.4);
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
  padding: 20px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  backdrop-filter: blur(5px);
}

.modal {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 20px;
  padding: 40px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  transform: scale(0.9);
  animation: modalSlideIn 0.3s ease forwards;
  border: 2px solid rgba(255, 255, 255, 0.2);
}

@keyframes modalSlideIn {
  to {
    transform: scale(1);
  }
}

.modal-content {
  text-align: center;
  color: white;
}

.success-icon {
  font-size: 4rem;
  margin-bottom: 20px;
  animation: bounce 1s infinite;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

.modal-content h2 {
  margin: 0 0 20px;
  font-size: 2.5rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.modal-content p {
  margin: 10px 0 20px;
  font-size: 1.2rem;
  opacity: 0.9;
}

.time-display {
  background: rgba(255, 255, 255, 0.2);
  padding: 15px;
  border-radius: 15px;
  margin: 20px 0;
}

.time-label {
  display: block;
  font-size: 1rem;
  opacity: 0.8;
  margin-bottom: 5px;
}

.time-value {
  font-size: 2rem;
  font-weight: bold;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.close-btn {
  margin-top: 20px;
  padding: 15px 30px;
  font-size: 16px;
  font-weight: bold;
  background: linear-gradient(45deg, #ff6b6b, #ee5a52);
  color: white;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(238, 90, 82, 0.4);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.close-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(238, 90, 82, 0.6);
}
</style>
