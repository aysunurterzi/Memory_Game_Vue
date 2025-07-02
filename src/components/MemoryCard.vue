<template>
  <div class="card" :class="{ flipped: isFlipped, matched: isMatched, disabled: disableClick }" @click="handleClick">
    <div class="card-inner">
      <div class="card-front">
        <div class="card-pattern"></div>
        <div class="question-mark">?</div>
      </div>
      <div class="card-back">
        <div class="image-container">
          <img v-if="image" :src="require(`@/assets/img/${image}.png`)" :alt="image" class="animal-image" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemoryCard',
  props: ['image', 'isFlipped', 'isMatched', 'disableClick'],
  methods: {
    handleClick() {
      if (!this.isMatched && !this.disableClick) {
        this.$emit('click');
      }
    }
  }
}
</script>

<style scoped>
.card {
  width: 120px;
  height: 120px;
  perspective: 1000px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.card:hover:not(.disabled):not(.matched) {
  transform: translateY(-5px);
}

.card.disabled {
  cursor: not-allowed;
  opacity: 0.7;
}

.card-inner {
  width: 100%;
  height: 100%;
  position: relative;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
  border-radius: 15px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

.card.flipped .card-inner,
.card.matched .card-inner {
  transform: rotateY(180deg);
}

.card.matched .card-inner {
  animation: matchPulse 0.6s ease;
}

@keyframes matchPulse {
  0% { transform: rotateY(180deg) scale(1); }
  50% { transform: rotateY(180deg) scale(1.1); }
  100% { transform: rotateY(180deg) scale(1); }
}

.card-front,
.card-back {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  backface-visibility: hidden;
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
}

.card-front {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border: 2px solid rgba(255, 255, 255, 0.3);
  position: relative;
  overflow: hidden;
}

.card-pattern {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(circle at 20% 50%, rgba(255, 255, 255, 0.1) 2px, transparent 2px),
    radial-gradient(circle at 80% 50%, rgba(255, 255, 255, 0.1) 2px, transparent 2px),
    radial-gradient(circle at 40% 20%, rgba(255, 255, 255, 0.1) 1px, transparent 1px),
    radial-gradient(circle at 60% 80%, rgba(255, 255, 255, 0.1) 1px, transparent 1px);
  background-size: 30px 30px;
  pointer-events: none;
}

.question-mark {
  font-size: 3rem;
  color: white;
  font-weight: bold;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  z-index: 1;
  position: relative;
  animation: questionPulse 2s infinite;
  line-height: 1;
}

@keyframes questionPulse {
  0%, 100% { opacity: 0.8; }
  50% { opacity: 1; }
}

.card-back {
  background: linear-gradient(135deg, #fff 0%, #f8f9fa 100%);
  border: 2px solid #e0e0e0;
  transform: rotateY(180deg);
  box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 8px;
}

.image-container {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.animal-image {
  max-width: calc(100% - 8px);
  max-height: calc(100% - 8px);
  width: auto;
  height: auto;
  object-fit: contain;
  object-position: center;
  filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.2));
  transition: all 0.3s ease;
  display: block;
  margin: auto;
}

.card.matched .animal-image {
  transform: scale(1.05);
  filter: drop-shadow(2px 2px 8px rgba(0, 0, 0, 0.3)) 
          drop-shadow(0 0 15px rgba(255, 215, 0, 0.6));
}

/* Mobile responsiveness */
@media (max-width: 768px) {
  .card {
    width: 80px;
    height: 80px;
  }
  
  .question-mark {
    font-size: 2rem;
  }
  
  .card-back {
    padding: 4px;
  }
  
  .animal-image {
    max-width: calc(100% - 4px);
    max-height: calc(100% - 4px);
  }
}

/* Ensure consistent sizing across different screen sizes */
@media (min-width: 769px) and (max-width: 1024px) {
  .card {
    width: 100px;
    height: 100px;
  }
  
  .question-mark {
    font-size: 2.5rem;
  }
  
  .card-back {
    padding: 6px;
  }
  
  .animal-image {
    max-width: calc(100% - 6px);
    max-height: calc(100% - 6px);
  }
}
</style>
