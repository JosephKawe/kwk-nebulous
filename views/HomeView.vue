<template>
    <StarsView />
    <NavbarView visibleSearch="hidden" class="z-40" />
    <main class="flex items-end w-full flex-col overflow-hidden h-screen lg:h-full bg-zinc-950 lg:text-white">
      <div class="overflow-hidden z-20 fixed top-[2%] lg:-left-[20%] lg:top-[3%] opacity-0 duration-[1000ms]" :class="{'opacity-100' : time}">
        <canvas class="z-30" ref="canvasRef"></canvas>
      </div>
      <section class="text-white py-[10%] lg:w-[50%] md:py-[5%] landscape:py-[1.5%] px-[10%] xl:pl-[7.5%] xl:pr-[10%] flex-col w-full flex justify-between lg:justify-center h-screen items-center lg:text-left text-center">
        <div class="flex flex-col text-mainColor z-20 mb-[5%]">
          <h1 class="text-5xl md:text-7xl 2xl:text-8xl z-10 xs:pt-[0.3em] sm:pt-[15%] md:pt-[10%] whitespace-nowrap font-bold tracking-widest uppercase duration-[2000ms] opacity-0 landscape:pt-[0%]" :class="{'opacity-100' : time}">KWK</h1>
          <h4 class="text-2xl uppercase tracking-[0.8em] opacity-0 font-extralight lg:text-4xl 2xl:text-5xl duration-[2000ms]" :class="{'opacity-100' : time}">Nebulous</h4>
          <p class="z-10 text-xs md:text-base xl:text-lg pt-[3%] lg:pt-[10%] 2xl:pt-[5%] opacity-0 duration-[3000ms]" :class="{'opacity-100' : time}">Desvende os mistérios do cosmos conosco! Explore o universo infinito, mergulhe em artigos fascinantes e guias práticos sobre astronomia. Prepare-se para uma jornada cósmica que expandirá seus horizontes e despertará sua curiosidade estelar."</p>
        </div>
        <div class="flex flex-col justify-center z-20 w-full items-center text-[#989898] lg:pt-[5%] lg:items-start mb-[28%] md:mb-[7.5em] lg:mb-[0%]">
          <p class="font-light md:text-2xl lg:text-xl md:font-normal tracking-wider opacity-0 duration-[4000ms]" :class="{'opacity-100' : time}">Rises the moon...</p>
          <div class="flex ml-[10%] lg:ml-[4em] items-center justify-center pt-[2%] gap-x-12 md:gap-x-[5em] lg:gap-x-[4em] landscape:gap-12 opacity-0 duration-[5000ms]" :class="{'opacity-100' : time}">
            <RouterLink class="z-10 flex justify-center" to="/astros">
              <button class="px-[40%] md:px-[50%] py-[10%] md:py-[12%] md:text-xl lg:text-base bg-transparent border-t-2 border-r-2 rounded-lg cursor-pointer select-none active:translate-y-2 hover:bg-[#7c7c7c] active:[box-shadow:0_0px_0_0_#656565,0_0px_0_0_#7c7c7c] active:border-b-[0px] active:border-t-[0px] active:border-r-[0px] transition-all duration-150 [box-shadow:-3px_3px_0_0_#7c7c7c] border-b-[2px] uppercase tracking-widest border-zinc-700 hover:text-zinc-950 landscape:text-xs">
                Explorar
              </button>
            </RouterLink>
            <button @click="toggleModal" class="relative group z-10 py-[5%] md:py-[5.5%] lg:py-[5%] text-center text-xl lg:text-lg flex justify-center items-center px-[9%] lg:px-[11%] md:text-2xl bg-transparent border-t-2 border-r-2 rounded-lg cursor-pointer select-none active:translate-y-2 hover:bg-[#7c7c7c] active:[box-shadow:0_0px_0_0_#656565,0_0px_0_0_#7c7c7c] active:border-b-[0px] active:border-t-[0px] active:border-r-[0px] transition-all duration-150 [box-shadow:-3px_3px_0_0_#7c7c7c] border-b-[2px] uppercase tracking-widest border-zinc-700 hover:text-zinc-950 landscape:text-xs">
              ?
              <div class="hidden lg:flex absolute z-50 -bottom-10 left-1/2 transform -translate-x-[10%] bg-[#989898] backdrop-blur-3xl text-zinc-950 text-sm px-2 py-1 rounded whitespace-no-wrap opacity-0 pointer-events-none transition-opacity duration-300 group-hover:opacity-100">
                Ver mais
              </div>
            </button>
          </div>
        </div>
      </section>
      <section :class="`${openModal ? 'flex' : 'hidden'} bg-black/40 px-[10%] backdrop-blur-md h-[70%] z-20 rounded-2xl -translate-x-1/2 -translate-y-1/2 top-[50%] left-[50%] absolute w-[80%] justify-start items-center flex-col`">
        <button @click="toggleModal" class="absolute font-extralight text-white right-[5%] md:right-[4%] top-[1%] md:top-[2%] text-3xl md:text-5xl">&times;</button>
        <div class="text-white flex justify-center gap-y-6 md:gap-y-10 items-center h-full flex-col">
          <h1 class="text-4xl md:text-8xl uppercase font-medium tracking-widest">Lua</h1>
          <div class="xs:text-[0.7em] 2xl:text-sm justify-center gap-4 flex flex-wrap 2xl:flex-nowrap 2xl:whitespace-nowrap">
            <span class="bg-white/10 px-[3%] rounded-full">Tamanho: 3.474km</span>
            <span class="bg-white/10 px-[3%] rounded-full">Idade: 4.5 Bilhões de Anos</span>
            <span class="bg-white/10 px-[3%] rounded-full">Tipo: Satélite Natural</span>
            <span class="bg-white/10 px-[3%] rounded-full">Material: Rocha e Regolito</span>
          </div>
          <p class="text-[0.7em] md:text-lg text-center">A Lua é uma figura celestial de grande importância, tanto para a ciência quanto para os apaixonados. Do ponto de vista científico, ela é um objeto de estudo essencial, fornecendo insights sobre a formação do sistema solar e desempenhando um papel crucial em fenômenos terrestres como as marés. Já para os românticos, a Lua representa promessas feitas sob seu brilho suave e sua beleza exuberante inspira poesia, arte e sonhos de amor. Assim, a Lua transcende seu status como um simples corpo celeste, tornando-se um símbolo poderoso para a humanidade.</p>
        </div>
        <h1 class="mb-[5%] text-center text-white text-sm lg:text-lg uppercase font-semibold tracking-wide">Deseja explorar outros Astros?</h1>
        <div class="flex text-white gap-x-6 mb-[10%] lg:text-2xl">
          <RouterLink to="/astros">
            <Button class="active:font-bold hover:font-bold duration-200 border-b-2 border-white">
              Sim
            </Button>
          </RouterLink>
          <Button class="active:font-bold hover:font-bold duration-200 border-b-2 border-white" @click="toggleModal">
            Não
          </Button>
        </div>
      </section>
    </main>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import * as THREE from "three";
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
import moonTexture from "../assets/Textura/ldem_3_8bit.jpg";
import moonDisplacementMap from "../assets/Textura/ldem_3_8bit.jpg";
import NavbarView from '@/components/NavbarView.vue';
import { RouterLink } from 'vue-router';
import StarsView from '@/components/StarsView.vue';

const openModal = ref<boolean>(false);
const time = ref<boolean>(false);
const canvasRef = ref<HTMLCanvasElement | null>(null);
const radius = ref<number>(2);
const scene = new THREE.Scene();
let geometry = THREE.SphereGeometry;
const textureLoader = new THREE.TextureLoader();
const texture = textureLoader.load(moonTexture);
const DisplacementMap = textureLoader.load(moonDisplacementMap);

const toggleModal = () => {
  openModal.value = !openModal.value;
}

const material = new THREE.MeshStandardMaterial({
  color: 0xffffff,
  map: texture,
  displacementMap: DisplacementMap,
  displacementScale: 0.05,
  bumpMap: DisplacementMap,
  bumpScale: 0.4,
});

let camera = new THREE.PerspectiveCamera;

onMounted(() => {
  setTimeout(() => {
    time.value = true;
  }, 200);

  const canvas = canvasRef.value;
  if (!canvas) {
    throw new Error("Elemento canvas não encontrado!");
  }

  const renderer = new THREE.WebGLRenderer({
    canvas: canvas,
    antialias: true,
    alpha: true
  });

  updateRadius(); 

  const w = window.innerWidth;
  const h = window.innerHeight;

  renderer.setSize(w, h);

  camera = new THREE.PerspectiveCamera(25, w / h);
  camera.position.set(10, 10, 25);
  scene.add(camera);

  geometry = new THREE.SphereGeometry(radius.value, 64, 64); 

  const mesh = new THREE.Mesh(geometry, material);
  scene.add(mesh);

  const controls = new OrbitControls(camera, canvas);
  controls.enableDamping = true;
  controls.enablePan = false;
  controls.enableZoom = true;

  const light = new THREE.DirectionalLight(0xffffff, 1);
  light.position.set(80, 25, 20)
  scene.add(light);

  window.addEventListener("resize", () => {
    updateRadius(); 
    const w = window.innerWidth;
    const h = window.innerHeight;

    camera.aspect = w / h;
    camera.updateProjectionMatrix();
    renderer.setSize(w, h);
  });

  const loop = () => {
    mesh.rotation.y += 0.001;
    renderer.render(scene, camera)
    window.requestAnimationFrame(loop);
  }

  loop();
});

function updateRadius() {
  if (window.innerWidth < 380) {
    radius.value = 1.7;
  }  else if (window.innerWidth < 768) {
    radius.value = 2.2;
  } else if (window.innerWidth < 1024) {
    radius.value = 2.6;
  } else if (window.innerWidth < 1280) {
    radius.value = 3.5;
  } else if (window.innerWidth < 1536) {
    radius.value = 4;
  } else if (window.innerWidth > 1536) {
    radius.value = 4.5;
  }
}

</script>

<style scoped>
.tooltip-btn {
  position: relative;
}

.tooltip-text {
  visibility: visible;
  width: 120px;
  background-color: black;
  color: white;
  text-align: center;
  padding: 5px 0;
  border-radius: 6px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  opacity: 100;
  transition: opacity 0.3s;
}

.tooltip-btn:hover .tooltip-text {
  visibility: visible;
  opacity: 1;
}
</style>
