<script setup lang="ts">
import { ref } from 'vue';
import catBeerImage from '@/assets/catbeer.png';

const noButton = ref<HTMLButtonElement | null>(null);
const step = ref(1)

const moveButton = () => {
  const button = noButton.value;
  if (button) {
    const container = button.parentElement;
    if (container) {
      const containerRect = container.getBoundingClientRect();
      const maxX = containerRect.width - button.offsetWidth;
      const maxY = containerRect.height - button.offsetHeight;

      let randomX, randomY;
      do {
        randomX = Math.random() * maxX;
        randomY = Math.random() * maxY;
      } while (
        Math.abs(randomX - parseFloat(button.style.left || '0')) < 50 ||
        Math.abs(randomY - parseFloat(button.style.top || '0')) < 50
      );

      button.style.position = 'absolute';
      button.style.left = `${randomX}px`;
      button.style.top = `${randomY}px`;
    }
  }
};

const accept = () => {
  step.value = 2;
};
</script>

<template>
  <div v-if="step === 1" class="container">
    <h1>maria, será que podemos ficar fofocando por videochamada
      enquanto tomamos uma cervejinha? 🍻🥰</h1>
    <div class="buttons">
      <button class="accept-button" @click="accept">bora!</button>
      <button
        ref="noButton"
        @mouseenter="moveButton"
        class="no-button"
      >
        vo nada
      </button>
    </div>
  </div>

  <div v-if="step === 2" class="container">
    <h2>kakaka eu sabia que você não iria resistir!</h2>
    <h3>
      já coloca esse grande evento na sua agenda, é só 
      <a href="https://calendar.app.google/sLti1z4Vp2EfcfEV6" target="_blank">clicar no link</a>
      !
    </h3>
    <h3>um beijo, linda! 🥰</h3>
    <img :src="catBeerImage" alt="Um gatinho bebendo cerveja" class="cat-image" />
  </div>
</template>

<style>
.container {
  text-align: center;
  margin-top: 10%;
  font-family: Arial, sans-serif;
  position: relative;
  min-height: 80vh;
}

h1 {
  font-size: 2rem;
  margin-bottom: 2rem;
}

.buttons {
  position: relative;
  width: 300px;
  height: 200px;
  margin: 0 auto;
}

.accept-button {
  background-color: #333;
  color: #ffffff;
}

button {
  padding: 10px 20px;
  font-size: 1rem;
  cursor: pointer;
  border: 2px solid #333;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #f0f0f0;
  color: #333;
}

.no-button {
  background-color: #ffcccc;
  position: absolute;
}

/* New CSS for the image on the second screen */
.cat-image {
  position: absolute;
  bottom: 5vh;
  left: 50%;
  transform: translateX(-50%);
  width: 250px;
  opacity: 0.9;
}
</style>
