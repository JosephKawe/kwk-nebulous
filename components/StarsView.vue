<!-- StarBackground.vue -->

<template>
    <div class="fixed w-full top-0 h-screen overflow-hidden bg-transparent">
      <div class="flex flex-col -mt-[15%]">
        <span
          v-for="(size, index) in starSizes"
          :key="index"
          class="bg-white mx-1 rounded-full shadowStar anim relative"
          :style="{
            '--i': index + 1,
            'width': size,
            'height': size,
            'animation-duration': `${getRandomDuration()}s`,
            'top': `${getRandomPosition()}vh`,
            'left': `${getRandomPosition()}vw`
          }"
        ></span>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue';
  
  const starSizes = ref<string[]>([]);
  
  onMounted(() => {
    // Gerar tamanhos aleatórios entre 1em e 10em para largura e altura de cada span
    starSizes.value = Array.from({ length: 250 }, () => `${Math.floor(Math.random() * 4) + 1}px`);
  });
  
  // Função para obter duração aleatória entre 5s e 15s
  const getRandomDuration = () => {
    return (Math.random() * 40 + 25).toFixed(2);
  };
  
  // Função para obter posição aleatória entre 0 e 100
  const getRandomPosition = () => {
    return (Math.random() * 100).toFixed(4);
  };
  </script>
  
  <style scoped>
  .shadowStar {
    box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.2),
                0 0 20px rgba(255, 255, 255, 0.2),
                0 0 40px rgba(255, 255, 255, 0.2);
  }
  
  .anim {
    animation: moveStars linear infinite;
  }
  
  @keyframes moveStars {
    0% {
      transform: translateX(-10vw);
    }
    100% {
      transform: translateX(120vw);
    }
  }
  </style>
  