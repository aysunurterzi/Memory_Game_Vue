<template>
  <div class="game-board">
    <div class="cards-grid">
      <MemoryCard
        v-for="card in cards"
        :key="card.id"
        :color="card.color"
        :is-flipped="card.isFlipped"
        :is-matched="card.isMatched"
        @click="handleCardClick(card)"
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
      cards: []
    }
  },
  created() {
    this.initializeGame()
  },
  computed: {
    shuffledColors() {
      return this.colors
        .concat(this.colors) // Her rengi iki kez ekleyerek eşleşmeleri sağlayın
        .sort(() => Math.random() - 0.5); // Renkleri karıştır
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
    },
    handleCardClick(card) {
      // Kart tıklanınca burada işlemler yapılacak
      console.log(`Clicked card id: ${card.id}, color: ${card.color}`);
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
