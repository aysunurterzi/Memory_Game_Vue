<template>
  <div class="card" :class="{ flipped: isFlipped, matched: isMatched }" @click="handleClick">
    <div class="card-inner">
      <div class="card-front"></div>
      <div class="card-back" :style="{ backgroundColor: isFlipped || isMatched ? color : 'transparent' }"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemoryCard',
  props: ['color', 'isFlipped', 'isMatched'],
  methods: {
    handleClick() {
      if (!this.isMatched) {
        this.$emit('click');
      }
    }
  }
}
</script>

<style scoped>
.card {
  width: 100px;
  height: 100px;
  margin: 5px;
}

.card-inner {
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.card.flipped .card-inner,
.card.matched .card-inner {
  transform: rotateY(180deg);
}

.card-front,
.card-back {
  width: 100%;
  height: 100%;
  position: absolute;
}

.card-front {
  background-color: grey; 
}

.card-back {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  color: white;
}
</style>
