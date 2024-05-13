
<template>
  <div @click="handleClick" :class="{ 'card': true, 'open': isOpen }">
    <img v-if="isOpen" :src="data.image" :alt="data.id">
  </div>
</template>

<script>
export default {
  props: {
    data: Object // Kart verisi
  },
  data() {
    return {
      isOpen: false // Kartın açık olup olmadığını belirten bayrak
    };
  },
  methods: {
    handleClick() {
      if (!this.isOpen) {
        this.$emit('select', this);
        this.isOpen = true;
      }
    }
  }
};
</script>

<style scoped>
.card {
  width: 100px;
  height: 100px;
  background-color: #ccc;
  display: inline-block;
  margin: 5px;
  cursor: pointer;
}

.open {
  background-color: #fff;
}
</style>
