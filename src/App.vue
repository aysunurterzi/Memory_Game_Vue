<template>
  <div>
    <button @click="startGame" v-if="!gameStarted">Oyuna Başla</button>
    <div class="board" v-else>
      <Card v-for="(card, index) in cards" :key="index" :data="card" @select="selectCard" />
    </div>
  </div>
</template>

<script>
import Card from './components/MemoryCard';

export default {
  components: {
    Card
  },
  data() {
    return {
      cards: [], 
      selectedCards: [], 
      gameStarted: false, 
      timer: null, 
      remainingTime: 60
    };
  },
  methods: {
    startGame() {
      
      this.gameStarted = true;
      this.startTimer();
      this.initializeCards();
    },
    startTimer() {
      this.timer = setInterval(() => {
        if (this.remainingTime > 0) {
          this.remainingTime--;
        } else {
          clearInterval(this.timer);
          alert("Oyun bitti!");
        }
      }, 1000);
    },
   initializeCards() {
      const animals = ['aslan', 'fil', 'kedi', 'kopek', 'ordek', 'tavsan', 'timsah', 'zurafa'];
      const shuffledAnimals = animals.concat(animals).sort(() => Math.random() - 0.5);
      this.cards = shuffledAnimals.map((animal, index) => ({
        id: index,
        image: require(`./assets/img/${animal}.png`), // varsayılan olarak assets klasöründe olduğunu varsayalım
        isOpen: false,
        matched: false
      }));
    },

selectCard(card) {
  if (card.isOpen || this.selectedCards.length === 2 || card.matched) {
    return;
  }

  this.selectedCards.push(card);
  card.isOpen = true;

  
  if (this.selectedCards.length === 2) {
    this.checkMatch();
  }
},


    checkMatch() {
      if (this.selectedCards[0].image === this.selectedCards[1].image) {
        setTimeout(() => {
          this.selectedCards.forEach(card => {
            card.isOpen = false;
          });
          this.selectedCards = [];
        }, 1000);
      } else {
        // Eşleşmeme durumu
        setTimeout(() => {
          this.selectedCards.forEach(card => {
            card.isOpen = false;
          });
          this.selectedCards = [];
        }, 1000);
      }
    }
  }
};
</script>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}
</style>
