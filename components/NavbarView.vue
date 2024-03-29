<template>
  <main class="flex justify-center items-center absolute w-full text-white">

    <!-- Botão para abrir/fechar o menu -->
    <button @click="toggleMenu"
      class="z-50 lg:hidden fixed pointer-events-auto duration-500 w-auto h-auto top-3 md:top-6 right-2.5 md:right-3.5"
      :class="{ '-translate-y-0': !isMenuOpen }">
      <!-- Linha superior do ícone -->
      <p class="h-[0.18em] md:h-[0.25em] w-6 md:w-9 duration-300 shadow-xl bg-white"
        :class="{ 'rotate-45 translate-y-3': !isMenuOpen }"></p>
      <!-- Linha do meio do ícone -->
      <p class="h-[0.18em] md:h-[0.25em] my-1.5 md:my-2 w-6 md:w-9 duration-300 shadow-xl bg-white"
        :class="{ 'hidden': !isMenuOpen }"></p>
      <!-- Linha inferior do ícone -->
      <p class="h-[0.18em] md:h-[0.25em] w-6 md:w-9 duration-300 shadow-xl bg-white"
        :class="{ '-rotate-45 translate-y-[0.57em]': !isMenuOpen }"></p>
    </button>

    <!-- Barra de navegação -->
    <header
      class="flex font-kanit justify-start z-40 opacity-100 lg:w-screen lg:px-[10.5%] fixed lg:relative items-start w-full top-0 overflow-x-hidden lg:justify-between lg:h-[9%] h-screen transX lg:transXR backdrop-blur-3xl lg:backdrop-blur-0 lg:items-center duration-500 lg:bg-transparent overflow-hidden"
      :class="{ 'lg:pointer-events-auto transXR': !isMenuOpen }">

      <nav
        class="w-full h-full flex-col lg:w-full flex justify-start lg:justify-between lg:translate-x-[0%] items-center lg:mt-[1.2%]  lg:flex-row lg:mb-[1.2%]"
        :class="{ 'duration-700': !isMenuOpen, 'w-full h-full overflow-hidden duration-700 opacity-100': isMenuOpen }">

        <div class="flex mt-[6em] items-center justify-center lg:mt-0">
          <RouterLink to="/" class="flex flex-col lg:flex-row items-center gap-x-2">
            <img src="/src/assets/KWK.png" class="w-20 lg:w-9" alt="KWK">
            <h1 class="lg:text-4xl font-semibold hidden lg:flex lg:mb-[3%] tracking-wider">KWK</h1>
          </RouterLink>

          <div :class="`flex ${visibleSearch}`">
            <!-- Lista de navegação -->
            <form :class="`lg:flex hidden items-center w-[20em] justify-center ml-[5%] ${visibleSearch}`">
              <label for="simple-search" class="sr-only">Search</label>
              <div class="relative w-full">
                <input type="text" v-model="searchQuery" @input="handleSearch" id="simple-search"
                  class="bg-white/20 text-sm focus:bg-transparent rounded-lg outline-none block w-full px-[8%] py-1 placeholder-white -outline-offset-2 focus:outline-white  duration-200"
                  placeholder="Pesquisar Planeta..." required>
              </div>
            </form>
          </div>
        </div>

        <ul
          class="lg:w-auto w-screen items-center gap-12 text-3xl md:text-4xl lg:text-lg 2xl:text-[1.2em] flex flex-col lg:flex-row justify-center mt-[4em] lg:mt-0">
          <!-- Loop pelas páginas para criar os links -->
          <li v-for="page in pages" :key="page.id" class="relative">
            <RouterLink :to="page.route"
              class="block uppercase my-1 px-5 text-decoration-none text-white font-sans text-2xl lg:text-lg transition-all duration-500 z-10 hover:text-zinc-950 custom-link font-normal">
              <h2 class="tracking-wide">{{ page.label }}</h2>
            </RouterLink>
          </li>
        </ul>
      </nav>

    </header>
  </main>
</template>

<script setup lang="ts">
import { ref, type Ref } from 'vue';
import { RouterLink } from 'vue-router';

const props = defineProps({
  onSearchChange: Function,
  visibleSearch: String
});

const searchQuery = ref('');

// Função para lidar com alterações no campo de pesquisa
const handleSearch = () => {
  // Verifica se a função de callback está definida antes de chamar
  if (props.onSearchChange) {
    props.onSearchChange(searchQuery.value);
  }
};

// Estado para controlar se o menu está aberto ou fechado
const isMenuOpen: Ref<boolean> = ref(!false);

// Função para alternar entre abrir e fechar o menu
function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}

// Interface para representar uma página na navegação
interface Page {
  id: string;
  route: string;
  label: string;
}

// Lista de páginas na navegação
const pages: Page[] = [
  { id: "home", route: "/", label: "Início" },
  { id: "astros", route: "/astros", label: "Astros" },
  { id: "sobre", route: "/about", label: "Sobre" },
  { id: "sobre", route: "/solarSystem", label: "Sistema Solar" },
];
</script>


<style scoped>
.custom-link::before,
.custom-link::after {
  content: '';
  position: absolute;
  transition: transform .3s, opacity .3s;
  z-index: -1;
}

.custom-link::before {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-top: 2px solid #fff;
  border-bottom: 2px solid #fff;
  transform: scaleY(2);
  opacity: 0;
}

.custom-link::after {
  top: 2px;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #fff;
  transform: scale(0);
  opacity: 0;
}

.custom-link:hover::before,
.custom-link:hover::after {
  transform: scaleY(1);
  opacity: 1;
}

@media (min-width: 320px) and (max-width: 1023px) {
  .transX {
    transform: translateX(100%);
  }

  .transXR {
    transform: translateX(0%);
  }
}
</style>