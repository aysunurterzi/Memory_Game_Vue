<template>
  <div class="game-board">
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
import MemoryCard from './MemoryCard.vue'

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
      disableClicks: false
    }
  },
  created() {
    this.initializeGame();
  },
  computed: {
    shuffledColors() {
      return this.colors
        .concat(this.colors) 
        .sort(() => Math.random() - 0.5); 
    }
  },
  methods: {
    initializeGame() {
      this.cards = this.shuffledColors.map((color, index) => ({
        id: index,
        color,
        isFlipped: false,
        isMatched: false
      }));
      this.flippedCards = [];
    },
    handleCardClick(index) {
      if (this.disableClicks) return;

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
    }
  }
}
</script>

<style scoped>
.game-board {
  display: flex;
  justify-content: center;
  align-items: center;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}
</style>
