<template>
  <!-- Background stars -->
  <StarsView class="z-10" />

  <!-- Navbar -->
  <NavbarView class="z-50" visibleSearch="hidden" />

  <!-- Main content -->
  <main class="flex flex-col justify-center overflow-hidden items-center w-full lg:h-screen bg-zinc-950">
    <section class="flex justify-center flex-col lg:flex-col items-center px-[5%] lg:px-[10%] mt-[20%] lg:mt-[2%] z-30 mb-[10%] lg:mb-0">
      <!-- Logo and title section -->
      <div class="flex items-center lg:gap-x-6 justify-center text-white">
        <div class="flex flex-col items-center lg:flex-row justify-between mb-[10%] md:mb-[5%] lg:mb-[4%]">
          <!-- Logo -->
          <img src="../assets/KWK.png" class="w-[25%] md:w-[30%] lg:w-[12%] object-contain mb-[1%] lg:-mb-[2%] opacity-0 duration-[500ms]" :class="{'opacity-100' : time}" alt="KWK">

          <!-- Title -->
          <div class="flex flex-col lg:-ml-[8%] text-center lg:text-left opacity-0 duration-[1000ms]" :class="{'opacity-100' : time}">
            <h1 class="text-5xl md:text-7xl 2xl:text-9xl z-10 whitespace-nowrap font-bold tracking-widest">KWK</h1>
            <h3 class="text-3xl uppercase tracking-[0.4em] font-extralight lg:text-4xl 2xl:text-6xl duration-200">NEBULOUS
            </h3>
          </div>

          <!-- Description -->
          <div class="flex justify-end flex-col lg:w-[45%] pt-[10%] md:pt-[7.5%] lg:-mb-[1.5%] lg:pt-0 text-center opacity-0 duration-[1500ms]" :class="{'opacity-100' : time}">
            <h1 class="font-bold lg:text-xl mb-[3%] md:mb-[1%]">Explorando os Planetas: Uma Viagem Cósmica com o KWK Nebulous</h1>
            <p class="text-sm lg:text-lg">Bem-vindo ao KWK Nebulous, sua plataforma dedicada à exploração dos planetas que povoam
              nosso fascinante sistema solar. Aqui, convidamos você a embarcar em uma jornada emocionante através do
              cosmos, mergulhando fundo nos mistérios e maravilhas de cada mundo celestial.</p>
          </div>
        </div>
      </div>

      <!-- About section -->
      <div class="flex flex-col text-center lg:text-left lg:justify-between bg-white/15 py-[5%] lg:py-[2%] px-[5%] lg:px-[3%] rounded-xl backdrop-blur-sm text-lg text-white">

        <div class="flex flex-col lg:flex-row justify-between mb-[2.5%] gap-y-6 lg:gap-0">
          <div class="lg:w-[40%] opacity-0 duration-[2000ms]" :class="{'opacity-100' : time}">
            <h1 class="text-base font-bold lg:text-lg mb-[2%] md:mb-[1%]">Sobre o KWK Nebulous: Desvende os Mistérios do
              Cosmos</h1>
            <p class="text-sm lg:text-base">Bem-vindo ao KWK Nebulous, seu portal pessoal para explorar os segredos do
              universo e
              desvendar os mistérios dos planetas. Aqui, mergulharemos fundo nas energias cósmicas que moldam nossas vidas
              e influenciam nossos destinos.</p>
          </div>
          <div class="hidden lg:flex bg-white h-full w-[0.05em] opacity-0 duration-[2750ms]" :class="{'opacity-100' : time}"></div>
          <div class="lg:w-[45%] opacity-0 duration-[2500ms]" :class="{'opacity-100' : time}">
            <h1 class="text-base font-bold lg:text-lg mb-[2%] md:mb-[1%]">Explorando os Planetas: Uma Viagem Cósmica com o KWK
              Nebulous</h1>
            <p class="text-sm lg:text-base">Cada planeta oferece uma riqueza de informações para explorar, desde dados
              científicos até curiosidades sobre sua história e mitologia. Se você é um entusiasta da astronomia, um
              estudante curioso ou apenas aprecia a beleza do cosmos, o KWK Nebulous é o seu destino para expandir seus
              horizontes.</p>
          </div>
        </div>


        <div class="flex my-[7.5%] md:my-[3%] lg:my-0 bg-white h-[0.08em] w-full"></div>

        <!-- Planets exploration section -->
        <div class="flex flex-col lg:flex-row pt-[2.5%] justify-center items-center lg:items-start opacity-0 duration-[3000ms]" :class="{'opacity-100' : time}">
          <div class="flex flex-col rounded-xl w-full lg:w-auto justify-center items-center lg:py-10 bg-black px-[12%] mb-[7.5%] md:mb-[4%] lg:mb-0">
            <img src="/src/assets/KWK.png" class="bg-black z-50 p-[5%] lg:py-[0%] lg:px-[12%] w-[8em] rounded-xl" alt="KWK Logo">
            <h1 class="font-semibold mt-[2%] md:mt-[0.2%]">Kohako</h1>
            <span class="mt-[2%] md:mt-[0.5%] lg:mt-[2%] text-sm">Ceo / Creator</span>
            <ul class="flex justify-end items-end gap-x-3 mt-[6%] mb-[10%] md:mb-[7.5%]">
              <li class="flex justify-end gap-4 items-center w-8 lg:w-8">
                <a href="https://github.com/kohakodev">
                  <img class="object-contain" src="/src/assets/github_rounded.png" alt="">
                </a>
              </li>
              <li class="flex justify-end gap-4 items-center w-8 lg:w-8">
                <a href="https://github.com/kohakodev">
                  <img class="object-contain" src="/src/assets/linkedin_rounded.png" alt="">
                </a>
              </li>
              <li class="flex justify-end gap-4 group items-center w-8 lg:w-8">
                <a href="https://github.com/kohakodev">
                  <img class="object-contain group-hover:invert" src="/src/assets/instagram_rounded.png" alt="">
                </a>
              </li>
            </ul>
          </div>
          
          <div class="text-white justify-between h-full flex w-full flex-col opacity-0 duration-[3500ms]" :class="{'opacity-100' : time}">
            <div class="text-white lg:text-left w-full lg:w-[90%] lg:ml-[4%] mb-[8%] lg:mb-[2.5%]">
              <h1 class="font-bold lg:text-lg pb-[2%] md:pb-[1%]">Sobre a KWK</h1>
              <p class="text-sm md:text-base">Olá, sou Kohako, o arquiteto deste mundo virtual que agora você explora. Para mim, o universo é uma fonte inesgotável de fascínio, uma sinfonia complexa de elementos entrelaçados. Cada aspecto desperta em mim uma profunda curiosidade, alimentando um desejo incessante por descoberta. Desde os primórdios da minha existência, busco desvendar seus segredos, decifrando os mistérios que o permeiam. Cada revelação intensifica minha dedicação em desvendar seus enigmas, impulsionando-me a buscar novos horizontes de conhecimento. É por isso que criei o KWK Nebulous, onde você pode explorar a grandiosidade deste universo.</p>
            </div>
            <div class="w-full lg:w-[90%] lg:ml-[4%] h-full flex gap-x-4 lg:gap-x-12 justify-between items-center mb-[2%]">
              <RouterLink to="/astros" class="w-[80%]">
                  <button class="text-xs lg:text-sm bg-transparent border-t-2 h-[4em] w-full border-r-2 rounded-lg cursor-pointer select-none active:translate-y-2 hover:bg-white active:[box-shadow:0_0px_0_0_#656565,0_0px_0_0_#fff] active:border-b-[0px] active:border-t-[0px] active:border-r-[0px] transition-all duration-150 [box-shadow:-3px_3px_0_0_#fff] border-b-[2px] border-zinc-400 hover:text-zinc-950">
                    Explorar
                  </button>
              </RouterLink>

              <a href="https://github.com/kohakodev" class="w-[80%]">
                <button class="text-xs lg:text-sm bg-transparent border-t-2 h-[4em] w-full border-r-2 rounded-lg cursor-pointer select-none active:translate-y-2 hover:bg-white active:[box-shadow:0_0px_0_0_#656565,0_0px_0_0_#7c7c7c] active:border-b-[0px] active:border-t-[0px] active:border-r-[0px] transition-all duration-150 [box-shadow:-3px_3px_0_0_#fff] border-b-[2px] border-zinc-400 hover:text-zinc-950">
                  Outros Projetos KWK
                </button>
              </a>
              
            </div>
          </div>
          
        </div>

      </div>

    </section>
  </main>
</template>

<script setup lang="ts">
import NavbarView from '@/components/NavbarView.vue';
import StarsView from '@/components/StarsView.vue';
import { onMounted, ref } from 'vue';
import { RouterLink } from 'vue-router';

const time = ref<boolean>(false)

onMounted(() => {
  setTimeout(() => {
    time.value = true;
  }, 200);
})

</script>
