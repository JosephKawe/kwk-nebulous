<script setup lang="ts">
import data from "../assets/Dados/data.json";
import NavbarView from '@/components/NavbarView.vue';
import StarsView from '@/components/StarsView.vue';
import { ref, onMounted, onBeforeUnmount, computed } from 'vue';

// Declaração de variáveis reativas
const cardsToShow = ref<number>(5);
const loading = ref<boolean>(false);
const searchQuery = ref<string>('');
const sortBy = ref<string>('');
const time = ref<boolean>(false);

// Carrega mais cartões
const loadMoreCards = () => {
  if (!loading.value) {
    loading.value = true;
    setTimeout(() => {
      cardsToShow.value += 5;
      loading.value = false;
    }, 1000);
  }
};

// Manipulador de rolagem
const handleScroll = () => {
  if (
    window.innerHeight + window.scrollY >= document.body.offsetHeight - 100 &&
    cardsToShow.value < data.planetas.length &&
    filteredAndSlicedPlanets.value.length >= 5
  ) {
    loadMoreCards();
  }
};

// Planetas filtrados e cortados
const filteredAndSlicedPlanets = computed(() => {
  const filteredPlanets = data.planetas.filter(planeta => {
    return planeta.nome.toLowerCase().includes(searchQuery.value.toLowerCase());
  });

  if (sortBy.value === 'tipo') {
    filteredPlanets.sort((a, b) => a.tipo.localeCompare(b.tipo));
  } else if (sortBy.value === 'idade') {
    filteredPlanets.sort(sortByAge);
  } else if (sortBy.value === 'alfabetica') {
    filteredPlanets.sort((a, b) => a.nome.localeCompare(b.nome));
  }

  return filteredPlanets.slice(0, cardsToShow.value);
});

// Evento montado
onMounted(() => {
  window.addEventListener('scroll', handleScroll);

  setTimeout(() => {
    time.value = true;
  }, 200);
});

// Evento antes de desmontar
onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});

// Atualiza a consulta de pesquisa
const updateSearchQuery = (newSearchQuery: string) => {
  searchQuery.value = newSearchQuery;
};

// Converte a idade para anos
const convertAgeToYears = (age: string): number => {
  const ageLower = age.toLowerCase();
  let multiplier = 1;

  if (ageLower.includes('bilhão') || ageLower.includes('bilhões')) {
    multiplier = 1000000000;
  } else if (ageLower.includes('milhão') || ageLower.includes('milhões')) {
    multiplier = 1000000;
  }

  const numericPart = parseFloat(ageLower.replace(/[^\d.-]/g, ''));
  return numericPart * multiplier;
};

// Ordena por idade
const sortByAge = (a: any, b: any): number => {
  const ageA = convertAgeToYears(a.idade);
  const ageB = convertAgeToYears(b.idade);

  if (ageA === ageB) {
    if (a.tipo < b.tipo) return -1;
    if (a.tipo > b.tipo) return 1;
    return 0;
  }

  return ageA - ageB;
};

// Manipulador para ordenar por
const handleSortBy = (event: Event) => {
  const selectedValue = (event.target as HTMLSelectElement).value;
  if (selectedValue) {
    sortBy.value = selectedValue;
  }
};

</script>

<template>
  <!-- Conteúdo principal -->
  <main :class="`flex flex-col justify-start z-10 pt-[15%] lg:pt-[0%] ${filteredAndSlicedPlanets.length == 1 ? 'h-screen md:h-auto' : 'h-auto'} ${filteredAndSlicedPlanets.length < 3 ? 'lg:h-screen' : 'md:h-auto'} pb-[5%] px-[10%] items-center w-full bg-zinc-950 overflow-hidden`">
    <!-- Componentes StarsView e NavbarView -->
    <StarsView />
    <NavbarView  :onSearchChange="updateSearchQuery" class="z-50" />

    <!-- Filtro de classificação -->
    <section class="w-full z-20 flex justify-center items-center mb-[5%] lg:mt-[8%] lg:mb-[2%] gap-3 lg:gap-6 opacity-0 duration-[1000ms]" :class="{'opacity-100' : time}">
      <div class="bg-white/20 backdrop-blur-3xl h-[0.2em] w-full"></div>
      <select @change="handleSortBy($event)" class="outline-none rounded-full text-xs hover:bg-zinc-950 lg:text-lg 2xl:text-base px-[0.1%] lg:px-[0.3%] py-[0.3%] uppercase bg-white/10 text-white backdrop-blur-3xl">
        <option class="bg-zinc-950" value="Filtrar">Filtrar</option>
        <option class="bg-zinc-950" value="tipo">Tipo</option>
        <option class="bg-zinc-950" value="alfabetica">A - Z</option>
      </select>
    </section>

    <!-- Formulário de pesquisa (para dispositivos móveis) -->
    <form class="flex items-center w-full justify-center lg:hidden mb-[3%]">
      <label for="simple-search" class="sr-only">Search</label>
      <div class="relative w-full">
        <input type="text" v-model="searchQuery" id="simple-search" class="bg-white/20 text-gray-900 md:text-base  focus:bg-transparent rounded-3xl outline-none block w-full px-[6%] p-1.5 md:p-2.5 dark:bg-white/20 dark:placeholder-white dark:text-white -outline-offset-2 focus:outline-white  duration-200" placeholder="Pesquisar Planeta..." required>
      </div>
    </form>

    <!-- Cartões de planetas -->
    <section v-for="item in filteredAndSlicedPlanets" :key="item.id" class="flex z-10 flex-col lg:flex-row items-center px-[3%] py-[8%] lg:py-[2%] justify-between bg-white/10 h-auto my-[4%] lg:my-[1.5%] rounded-3xl backdrop-blur-sm opacity-0 duration-[3000ms]" :class="{'opacity-100' : time}">
      <!-- Imagem do planeta -->
      <img :class="`w-[70%] rounded-full lg:w-[20%] 2xl:w-[15%] lg:ml-[1%] mb-[5%] lg:mb-0 ${item.nome.includes('Cometa') ? 'rounded-full' : ''} ${item.nome.includes('Nebulosa') ? 'rounded-full' : ''}`" :src="`/src/assets/Astros/${item.image}`" :alt="`astro: ${item.nome}`">

      <!-- Detalhes do planeta -->
      <div class="flex flex-col lg:ml-[2%] xl:ml-[0.2%] text-white lg:w-[60%] 2xl:w-[70%]">
        <h1 class="text-4xl md:text-5xl lg:text-4xl 2xl:text-5xl 2xl:mb-[1%] text-center lg:text-start font-medium mb-[10%] lg:mb-[2%]">{{ item.nome }}</h1>
        <p class="mb-[1.5%] text-[0.9em] xl:text-lg 2xl:text-lg hidden lg:flex">{{ item.resumo }}</p>
        <div class="flex flex-col lg:flex-row items-center lg:items-start whitespace-nowrap gap-y-2 lg:gap-x-[1%] text-zinc-900 font-semibold mb-[15%] lg:mb-[2%] text-sm md:text-base lg:text-xs 2xl:text-sm lg:font-bold">
          <h1 class="bg-white/80 inline px-[5%] lg:px-[1.5%] py-[0.2%] rounded-full">{{ item.tipo }}</h1>
          <h1 class="bg-white/80 inline px-[5%] lg:px-[1.5%] py-[0.2%] rounded-full">{{ item.composicao }}</h1>
          <h1 class="bg-white/80 inline px-[5%] lg:px-[1.5%] py-[0.2%] rounded-full">{{ item.idade }}</h1>
        </div>
      </div>

      <!-- Botão "Ver" -->
      <RouterLink :to="`details/${item.id}`">
        <button class="text-zinc-900 bg-white/80 text-xl md:text-2xl lg:text-xl 2xl:text-2xl px-[1.7em] lg:px-[1.5em] py-[0.3em] lg:py-[0.3em] uppercase font-semibold rounded-3xl md:rounded-full hover:-outline-offset-0 outline-white/80 outline hover:bg-transparent hover:text-white/80 duration-200">
          Ver
        </button>
      </RouterLink>
    </section>

    <!-- Indicador de carregamento -->
    <div v-if="loading">
      <h2 class="text-xl text-white tracking-wide">{{ filteredAndSlicedPlanets.length + ' / ' + data.planetas.length }}</h2>
    </div>
    <div v-if="loading" class="flex flex-col justify-center items-center my-[1.5%]">
      <article class="md:h-12 md:w-12 h-10 w-10 border-4 rounded-full animate-spin border-l-white border-r-white border-b-white border-t-gray-600"></article>
    </div>
  </main>
</template>
