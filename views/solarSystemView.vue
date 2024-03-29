<script setup lang="ts">
import NavbarView from '@/components/NavbarView.vue';
import StarsView from '@/components/StarsView.vue';
import data from "../assets/Dados/data.json";
import { onMounted, ref } from 'vue';


interface Planeta {
  nome: string;
  tamanho: string;
  composicao: string;
  distancia_da_terra: string;
  idade: string;
  id: number;
  resumo: string;
  tipo: string;
  image: string;
  sistemaSolar: boolean;
  orbita_ao_redor?: string;
  universo_ou_constelacao?: string;
}

const planetas = ref<Planeta[]>([]);
const planetasVisiveis = ref<Planeta[]>([]);
const planetasRestantes = ref<Planeta[]>([]);
const mostrarModal = ref(false);
const time = ref<boolean>(false)

onMounted(() => {
  setTimeout(() => {
    time.value = true;
  }, 200);
})

// Função para carregar os planetas
const carregarPlanetas = () => {
  // Aqui você deve carregar todos os planetas
  // por exemplo, você pode fazer uma requisição AJAX
  // ou carregar os dados de um arquivo JSON
  planetas.value = data.planetas;

  // Exibe os primeiros 5 planetas
  planetasVisiveis.value = planetas.value.slice(0, 5);

  // Armazena os planetas restantes
  planetasRestantes.value = planetas.value.slice(5);
};
// Carrega os planetas ao montar o componente
carregarPlanetas();

const abrirModal = () => {
  mostrarModal.value = true;
};

const fecharModal = () => {
  mostrarModal.value = false;
};

</script>

<template>
  <StarsView/>
  <NavbarView visibleSearch="hidden" class="z-40" />
  <main class="sm:h-screen flex flex-col w-full overflow-hidden lg:items-end items-center justify-center 2xl:justify-center bg-zinc-950 xs:h-auto">
    <h1 class="flex md:hidden uppercase font-bold absolute xs:top-[10%] overflow-hidden sm:top-[6%] tracking-widest text-white text-3xl rounded-full px-[3%] py-[1.5%] bg-white/10 backdrop-blur-3xl opacity-0 duration-[1000ms]" :class="{'opacity-100' : time}">Sistema Solar</h1>
    <section class="overflow-hidden opacity-0 duration-[2000ms]" :class="{'opacity-100' : time}">
      <div
        class="h-[40px] md:h-[80px] w-[40px] md:w-[80px] rounded-full bg-cover absolute left-[50%] lg:left-[24.5%] xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/astros/sun.png')]">
      </div>
      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[60px] md:h-[120px] w-[60px] md:w-[120px]">
        <div
          class="h-[7px] md:h-[14px] w-[7px] md:w-[14px] rounded-full bg-cover absolute left-[44%] top-[43%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/mercurio.png')] orbit-mercury">
          <p class="paragraph">Mercurio</p>
        </div>
      </div>

      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[100px] md:h-[180px] w-[100px] md:w-[180px]">
        <div
          class="h-[12px] md:h-[24px] w-[12px] md:w-[24px] rounded-full bg-cover absolute left-[45%] top-[45%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/venus.png')] orbit-venus">
          <p class="paragraph">Venus</p>
        </div>
      </div>

      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[140px] md:h-[240px] w-[140px] md:w-[240px]">
        <div
          class="h-[17px] md:h-[34px] w-[17px] md:w-[34px] rounded-full bg-cover absolute left-[44%] top-[44%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/terra.png')] orbit-earth">
          <div
            class="h-[33px] md:h-[50px] w-[33px] md:w-[50px] border border-dotted border-white relative left-[-8px] top-[-8px] rounded-full">
            <div
              class="h-[5px] w-[5px] rounded-full bg-cover absolute left-[45%] top-[45%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/lua.png')] orbit-moon">
            </div>
            <p class="paragraph">Terra</p>
          </div>
        </div>
      </div>

      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[180px] md:h-[300px] w-[180px] md:w-[300px]">
        <div
          class="h-[9px] md:h-[18px] w-[9px] md:w-[18px] rounded-full bg-cover absolute left-[47%] top-[46.5%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/marte.png')] orbit-mars">
          <p class="paragraph">Marte</p>
        </div>
      </div>

      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[220px] md:h-[360px] w-[220px] md:w-[360px]">
        <div
          class="h-[15px] md:h-[30px] w-[15px] md:w-[30px] rounded-full bg-cover absolute left-[47%] lg:left-[46%] top-[47%] lg:top-[46%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/jupiter.png')] orbit-jupiter">
          <p class="paragraph">jupiter</p>
        </div>
      </div>

      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[260px] md:h-[420px] w-[260px] md:w-[420px]">
        <div
          class="h-[22px] md:h-[44px] w-[22px] md:w-[44px] rounded-full bg-cover absolute left-[45%] top-[45%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/saturno.png')] orbit-saturn">
          <p class="text-right paragraph">Saturno</p>
        </div>
      </div>

      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[300px] md:h-[480px] w-[300px] md:w-[480px]">
        <div
          class="h-[17px] md:h-[34px] w-[17px] md:w-[34px] rounded-full bg-cover absolute left-[47%] lg:left-[46%] top-[47%] lg:top-[46%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/urano.png')] orbit-uranus">
          <p class="paragraph">Urano</p>
        </div>
      </div>

      <div
        class="rounded-full border border-dotted border-gray-200 absolute xs:top-[21em] sm:top-[35%] md:top-[31%] lg:top-[50%] left-[50%] lg:left-[24.5%] -translate-x-1/2 -translate-y-1/2 h-[340px] md:h-[540px] w-[340px] md:w-[540px]">
        <div
          class="h-[17px] md:h-[34px] w-[17px] md:w-[34px] rounded-full bg-cover absolute left-[47.5%] lg:left-[46.5%] top-[47.5%] lg:top-[46.5%] -translate-x-1/2 -translate-y-1/2 bg-[url('/src/assets/Astros/neturno.png')] orbit-neptune">
          <p class="paragraph">Neturno</p>
        </div>
      </div>

    </section>
    <section
      class="w-[80%] lg:w-[40%] flex flex-col items-center justify-start text-center mb-[12.5%] min-[2000px]:mr-[7.5%] lg:mr-[10%] md:mb-[7.5%] lg:mb-[0%] bg-white/10 backdrop-blur-sm rounded-xl xs:py-[10%] sm:py-[7.5%] md:py-[5%] px-[5%] xs:mt-[35em] sm:mt-[135%] md:mt-[85%] lg:mt-0 opacity-0 duration-[3000ms]" :class="{'opacity-100' : time}">
      <h1 class="text-white px-[1%] text-[0.9em] mb-[1%] md:text-2xl lg:text-lg 2xl:text-2xl uppercase font-bold tracking-wide">Sobre o nosso Sistema solar</h1>
      <p class="text-white px-[1%] text-[0.7em] md:text-base lg:text-sm 2xl:text-lg mb-[6%] font-light">O sistema solar é composto por um
        conjunto
        de corpos celestes que orbitam em torno do Sol, uma estrela de médio porte.</p>
      <h1 class="text-white px-[1%]  text-[0.9em] mb-[1%] md:text-2xl lg:text-lg 2xl:text-2xl uppercase font-bold tracking-wide">Localização</h1>
      <p class="text-white px-[1%] text-[0.7em] md:text-base lg:text-sm 2xl:text-lg font-light mb-[6%]">Localizado no Braço de Órion da Via
        Láctea,
        a cerca de 25.000 anos-luz do centro galáctico, o sistema solar é apenas um entre bilhões de sistemas planetários
        que orbitam ao redor do núcleo da galáxia.</p>
      <h1 class="text-white px-[1%] text-[0.9em] mb-[5%] md:text-2xl lg:text-lg 2xl:text-2xl uppercase font-bold tracking-wide">Planetas do Sistema Solar</h1>
      <section class="flex items-center">
        <!-- Renderiza os primeiros 5 planetas do sistema solar -->
        <template v-for="planeta in planetasVisiveis" :key="planeta.id">
          <div v-if="planeta.sistemaSolar" class="flex justify-center items-center mx-2">
            <div class="flex justify-center items-center">
              <RouterLink :to="`details/${planeta.id}`">
                <img class="w-7 md:w-12 object-contain" :src="`/assets/Astros/${planeta.image}`" :alt="planeta.nome">
              </RouterLink>
            </div>
          </div>
        </template>

        <!-- Mostra o "+" se houver mais planetas do sistema solar -->
        <div v-if="planetasRestantes.length > 0" class="flex font-black justify-center items-center text-xs mx-2 md:mx-3 md:text-xl md:mb-1">
          <span class="text-white cursor-pointer" @click="abrirModal">+</span>
        </div>
      </section>
    </section>
    <!-- Modal -->
    <div v-if="mostrarModal"
    class="fixed z-50 top-0 left-0 w-full h-full flex items-center flex-wrap bg-black backdrop-blur-[5px] justify-center bg-opacity-50 lg:flex-col">
    <h2 class="text-2xl md:text-4xl -mb-[15%] lg:mb-[3%] font-bold text-white z-50">Todos os planetas</h2>
    <button @click="fecharModal" class="absolute top-1 text-3xl md:text-5xl right-3 text-white hover:text-gray-700">&times;</button>
    <!-- Renderiza apenas os planetas do sistema solar -->
    <div class="bg-white/20 p-8 rounded-l-xl w-[80%] h-[80%] lg:h-[75%] flex-wrap overflow-y-scroll lg:overflow-hidden lg:rounded-xl flex items-center justify-center">
        <div class="grid xs:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 2xl:grid-cols-5 gap-4 gap-y-4 md:gap-6 2xl:gap-10">
            <div v-for="planeta in planetas.filter(planeta => planeta.sistemaSolar)" :key="planeta.id"
                class="flex justify-center">
                <RouterLink :title="`Detalhes sobre ${planeta.nome}`" :to="`details/${planeta.id}`" v-if="planeta.sistemaSolar"
                    class="justify-center flex-col lg:flex-row items-center lg:justify-start lg:gap-x-2 border-white/60 border-2 backdrop-blur-3xl rounded-2xl w-full h-[100%] 2xl:flex-col p-[1em] flex mb-1 mr-1 z-50 2xl:justify-center 2xl:items-center 2xl:px-[2em]
                    
                    
                    active:translate-y-2 hover:bg-[#7c7c7c] active:[box-shadow:0_0px_0_0_#656565,0_0px_0_0_#7c7c7c]
                    active:border-b-[0px] active:border-t-[0px] active:border-r-[0px]
                    transition-all duration-150 md:[box-shadow:-5px_5px_0_0_#7c7c7c] [box-shadow:-3px_3px_0_0_#7c7c7c]
                    border-b-[2px] tracking-widest border-zinc-700 hover:text-zinc-950
                    ">
                    <img class="xs:w-[2em] sm:w-[2.5em] md:w-[3em] 2xl:w-[4.6em] xs:mb-[0.5em] object-contain"
                        :src="`/assets/Astros/${planeta.image}`" :alt="planeta.nome">
                    <div class="text-center">       
                        <h2 class="xs:text-xs md:text-base lg:text-sm 2xl:text-xl xl:text-base font-bold text-white tracking-wide uppercase">{{ planeta.nome }}</h2>
                        <h6 class="xs:text-[0.6em] md:text-sm lg:text-xs 2xl:text-lg text-white font-thin tracking-wide whitespace-nowrap lg:whitespace-normal">{{ planeta.tipo.split("(")[0] }}</h6>
                    </div>
                </RouterLink>
            </div>
        </div>
    </div>
</div>


  </main>
</template>

<style scoped>
.orbit-mercury {
  animation: orbit2 2s linear infinite;
}

.orbit-venus {
  animation: orbit3 10s linear infinite;
}

.orbit-earth {
  animation: orbit4 20s linear infinite;
}

.orbit-moon {
  animation: orbit5 3s linear infinite;
}

.orbit-mars {
  animation: orbit6 30s linear infinite;
}

.orbit-jupiter {
  animation: orbit7 45s linear infinite;
}

.orbit-saturn {
  animation: orbit8 60s linear infinite;
}

.orbit-uranus {
  animation: orbit9 200s linear infinite;
}

.orbit-neptune {
  animation: orbit10 400s linear infinite;
}

@media (min-width: 320px) and (max-width: 768px) {
  @keyframes orbit2 {
    from {
      transform: rotate(0deg)translateX(30px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(30px) rotate(-360deg);
    }
  }

  @keyframes orbit3 {
    from {
      transform: rotate(0deg)translateX(50px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(50px) rotate(-360deg);
    }
  }

  @keyframes orbit4 {
    from {
      transform: rotate(0deg)translateX(70px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(70px) rotate(-360deg);
    }
  }

  @keyframes orbit5 {
    from {
      transform: rotate(0deg)translateX(18px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(18px) rotate(-360deg);
    }
  }

  @keyframes orbit6 {
    from {
      transform: rotate(0deg)translateX(90px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(90px) rotate(-360deg);
    }
  }

  @keyframes orbit7 {
    from {
      transform: rotate(0deg)translateX(108px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(108px) rotate(-360deg);
    }
  }

  @keyframes orbit8 {
    from {
      transform: rotate(0deg)translateX(130px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(130px) rotate(-360deg);
    }
  }

  @keyframes orbit9 {
    from {
      transform: rotate(0deg)translateX(150px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(150px) rotate(-360deg);
    }
  }

  @keyframes orbit10 {
    from {
      transform: rotate(0deg)translateX(170px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(170px) rotate(-360deg);
    }
  }
}

@media (min-width: 769px) {
  @keyframes orbit2 {
    from {
      transform: rotate(0deg)translateX(60px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(60px) rotate(-360deg);
    }
  }

  @keyframes orbit3 {
    from {
      transform: rotate(0deg)translateX(90px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(90px) rotate(-360deg);
    }
  }

  @keyframes orbit4 {
    from {
      transform: rotate(0deg)translateX(120px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(120px) rotate(-360deg);
    }
  }

  @keyframes orbit5 {
    from {
      transform: rotate(0deg)translateX(18px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(18px) rotate(-360deg);
    }
  }

  @keyframes orbit6 {
    from {
      transform: rotate(0deg)translateX(150px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(150px) rotate(-360deg);
    }
  }

  @keyframes orbit7 {
    from {
      transform: rotate(0deg)translateX(180px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(180px) rotate(-360deg);
    }
  }

  @keyframes orbit8 {
    from {
      transform: rotate(0deg)translateX(210px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(210px) rotate(-360deg);
    }
  }

  @keyframes orbit9 {
    from {
      transform: rotate(0deg)translateX(242px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(242px) rotate(-360deg);
    }
  }

  @keyframes orbit10 {
    from {
      transform: rotate(0deg)translateX(270px) rotate(0deg);
    }

    to {
      transform: rotate(360deg)translateX(270px) rotate(-360deg);
    }
  }
}



.paragraph {
  color: white;
  position: absolute;
  left: -30px;
  top: 15px;
  font-size: 0.8em;
  font-weight: 500;
}
</style>