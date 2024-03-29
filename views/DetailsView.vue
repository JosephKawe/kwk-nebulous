<script setup lang="ts">
import { onMounted, ref, watch } from 'vue';
import { useRoute } from 'vue-router';
import data from "../assets/Dados/data.json";
import NavbarView from '@/components/NavbarView.vue';
import StarsViewVue from '@/components/StarsView.vue';

const astroId = ref<number | null>(null);
const astro = ref<any>(null);
const loading = ref(true);
const time = ref<boolean>(false)

const route = useRoute();

onMounted(() => {

  setTimeout(() => {
    time.value = true;
  }, 200);

  watch(
    () => route.params.id,
    (newId: string | string[]) => {
      if (Array.isArray(newId)) {
        // Lógica para lidar com um array de strings, se necessário
      } else {
        // Lógica para lidar com uma string
        updateAstroId(newId);
        loadProject();
      }
    },
    { immediate: true }
  );
});

const updateAstroId = (newId: string | number | null) => {
  if (typeof newId === 'string') {
    const numId = parseInt(newId, 10);
    astroId.value = isNaN(numId) ? null : numId;
  } else if (typeof newId === 'number') {
    astroId.value = newId;
  } else {
    astroId.value = null;
  }
};

const loadProject = () => {
  loading.value = true;

  try {
    if (data && data.planetas && data.planetas_curiosidades) {
      const foundProject = data.planetas.find((project) => project.id === astroId.value);

      if (foundProject) {
        astro.value = {
          ...foundProject,
          curiosidades: data.planetas_curiosidades.filter((cur) => cur.id === astroId.value)
        };
        console.log(astro.value.tipo.slice(0, 6))
      } else {
        console.error('Projeto não encontrado para o ID:', astroId.value);
      }
    } else {
      console.error('Formato de dados inválido em data.json');
    }
  } catch (error) {
    console.error('Erro ao carregar o projeto:', error);
  } finally {
    loading.value = false;
  }

};

</script>

<template>
  <main
    class="bg-zinc-950 flex justify-center items-center h-auto lg:h-screen px-[10%] lg:px-[5%] xl:px-[10%] overflow-hidden lg:w-auto">
    <StarsViewVue />
    <NavbarView visibleSearch="hidden" class="z-50 top-0" />
    <section v-if="loading" class="flex flex-col justify-center items-center z-20">
      <article
        class="md:h-12 md:w-12 h-10 w-10 border-4 rounded-full animate-spin border-l-white border-r-white border-b-white border-t-gray-600 mb-[10%]">
      </article>
      <h2 class="text-white text-xl md:text-2xl animate-pulse">Carregando...</h2>
    </section>
    <section v-else class="z-20 flex items-center flex-col mt-[25%] md:mt-[15%] lg:mt-0 lg:flex-row justify-between">
      <section class="flex flex-col lg:flex-row items-center justify-center lg:mb-[7%]">
        <div class="lg:h-[20em] lg:w-[20em] 2xl:w-[35em] 2xl:h-[35em] 2xl:mr-[2%] mb-[10%] md:mb-[5%] lg:mb-0 lg:px-0">
          <h1
            class="text-center md:text-6xl lg:text-5xl text-5xl 2xl:text-7xl mb-[5%] text-white font-black tracking-wide uppercase lg:whitespace-nowrap opacity-0 duration-[1000ms]" :class="{'opacity-100' : time}">
            {{ astro.nome }}</h1>
          <img
            class="opacity-0 duration-[2000ms]"
            :class="`w-[100%] ${astro.nome.includes('Cometa') ? 'rounded-full' : ''} ${astro.nome.includes('Nebulosa') ? 'rounded-full' : ''} ${astro.tipo.includes('Buraco') ? 'rounded-full' : ''} ${astro.tipo.includes('Blazar') ? 'rounded-full' : ''} ${astro.tipo.includes('Sistema') ? 'rounded-full' : ''} ${astro.tipo.includes('supernova') ? 'rounded-full' : ''} ${astro.tipo.includes('Quasar') ? 'rounded-full' : ''} ${astro.tipo.includes('Tidal') ? 'rounded-full' : ''} ${astro.tipo.includes('Nebulosa') ? 'rounded-full' : ''} ${time ? 'opacity-100' : ''} object-contain`"
            :src="`/src/assets/Astros/${astro.image}`" :alt="`${astro.nome}`">
        </div>
        <div class="w-auto mb-[10%] md:mb-[5%] lg:mb-0 opacity-0 duration-[3000ms]" :class="{'opacity-100' : time}">
          <ul
            class="text-white lg:mt-[50%] 2xl:mt-[90%] flex flex-col items-center md:flex-row lg:flex-col gap-x-2 flex-wrap justify-center lg:justify-start lg:items-start lg:gap-12 whitespace-nowrap lg:text-sm">
            <li><span class="font-extrabold">Tamanho:</span> {{ astro.tamanho }}</li>
            <li class="lg:ml-[10%]"><span class="font-extrabold">Composição:</span> {{ astro.composicao }}</li>
            <li class="lg:ml-[15%]"><span class="font-extrabold">Distancia da Terra:</span> {{ astro.distancia_da_terra
              }}
            </li>
            <li class="lg:ml-[10%]"><span class="font-extrabold">Idade:</span> {{ astro.idade }}</li>
            <li><span class="font-extrabold">Tipo:</span> {{ astro.tipo }}</li>
          </ul>
        </div>
      </section>
      <div class="w-full h-[0.15em] rounded-full mb-[6%] bg-white lg:hidden"></div>
      <section class="justify-end flex flex-col text-white 2xl:px-0 2xl:w-[35%] lg:pt-[5%] opacity-0 duration-[4000ms]" :class="{'opacity-100' : time}">
        <h1 class="text-2xl md:text-3xl lg:text-2xl font-black tracking-wide uppercase text-center">Informações
        </h1>

        <div class="mb-[10%] lg:ml-[10%] mr-[5%] lg:translate-x-5 2xl:mx-0 lg:mb-10" v-for="item in astro.curiosidades"
          :key="item.id">
          <template v-for="[key, value] in Object.entries(item)">
            <h2 class="font-extrabold mt-[4%] text-ms md:text-lg lg:text-ms 2xl:text-base" v-if="key.includes('titulo')"
              v-bind:key="key">
              {{ value }}:
            </h2>
            <p class="text-xs md:text-sm lg:text-xs 2xl:text-sm" v-if="key.includes('resumo')" v-bind:key="key">{{ value
              }}</p>
          </template>
        </div>
      </section>
    </section>
  </main>
</template>
