<script setup>
import { computed, onMounted } from 'vue';
import { Swiper } from 'swiper';
import { EffectCoverflow, Autoplay } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/effect-coverflow';
import { getProjects } from '@/services/projectService';

const projects = computed(() => getProjects());
onMounted(() => {
  new Swiper('.swiper', {
    modules: [EffectCoverflow, Autoplay],
    effect: 'coverflow',
    speed: 1000,
    loop: true,
    direction: 'vertical',
    slidesPerView: 1,
    initialSlide: 0,
    mousewheelControl: true,
    coverflow: {
      rotate: 0,
      stretch: 150,
      depth: 200,
      modifier: 1,
      slideShadows: false
    },
    autoplay: true
  });
});
</script>

<template>
  <section class="flex w-full flex-col py-5">
    <div class="flex-1 flex justify-center flex-col items-center w-full lg:gap-8 gap-4">
      <div class="flex flex-col w-full items-center justify-center px-8 lg:flex-row gap-6">
        <div class="flex flex-col items-center lg:items-start lg:gap-3">
          <span class="text-[#8095AB]">Olá, eu sou</span>
          <h1 class="text-[25pt] lg:text-[40pt] font-semibold tracking-tighter text-white typewriter-animation typewriter-text max-w-fit">Meena Hiwatashi</h1>
          <p class="text-[#7fcaff] text-center w-[350px] lg:w-[520px] lg:text-start text-[13pt]">Sou uma desenvolvedora de software focada na resolução de problemas e na entrega de sistemas completos.</p>
        </div>
        <div class="lg:max-w-xl">
          <div class="swiper w-full lg:h-80 h-56">
            <div class="swiper-wrapper">
              <div class="swiper-slide rounded-lg bg-black w-full overflow-hidden px-6 border-[#1E2D3D] border" v-for="(project, index) in projects" :key="index">
                <div class="h-12 flex items-center">
                  <span class="text-[#E8B44F] font-semibold">{{ project.title }}</span>
                </div>
                <div>
                  <img :src="project.src" :srcset="project.srcset" sizes="(max-width: 600px) 480px, (max-width: 1200px) 800px, 1512px" :alt="project.title" :loading="project.src === '/images/projects/wire-cotton-800w.webp' ? 'eager' : 'lazy'" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="flex flex-col gap-6 pt-4">
        <div class="flex items-center flex-col gap-y-2">
          <img src="/images/me.webp" alt="" class="object-cover rounded-full w-16 h-16 border-[3.5px] border-[#303a4b]" />
          <a href="https://calendar.app.google/uCHpaj5xdWvwM3YBA" target="_blank" class="h-[29px] text-sm btn btn-primary">solicitar_contato</a>
        </div>
        <a class="btn btn-primary" href="https://github.com/MeenaMisae/portfolio" target="_blank">
          Gostou? Clona pra você!
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#70879E" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="7" y1="17" x2="17" y2="7"></line>
            <polyline points="7 7 17 7 17 17"></polyline>
          </svg>
        </a>
      </div>
    </div>
  </section>
</template>
<style scoped>
.typewriter-text {
  width: fit-content;
  border-right: 3px solid rgba(255, 255, 255, 0.75);
  white-space: nowrap;
  overflow: hidden;
  padding-right: 2px;
}

.typewriter-animation {
  animation:
    typewriter 3.5s steps(40) 1s 1 normal both,
    blinkTextCursor 800ms steps(40) infinite normal;
}

.css-blurry-gradient-blue {
  position: fixed;
  bottom: 25%;
  right: 5%;
  width: 300px;
  height: 300px;
  border-radius: 0% 0% 50% 50%;
  rotate: 10deg;
  filter: blur(70px);
  background: radial-gradient(circle at 50% 50%, rgba(77, 91, 206, 1), rgba(76, 0, 255, 0));
  opacity: 0.5;
  z-index: 10;
}

.css-blurry-gradient-green {
  position: absolute;
  top: 20%;
  right: 20%;
  width: 300px;
  height: 300px;
  border-radius: 0% 50% 0% 50%;
  filter: blur(70px);
  background: radial-gradient(circle at 50% 50%, rgba(67, 217, 173, 1), rgba(76, 0, 255, 0));
  opacity: 0.5;
  z-index: 10;
}

@keyframes typewriter {
  from {
    width: 0;
  }

  to {
    width: 100%;
  }
}

@keyframes blinkTextCursor {
  from {
    border-right-color: rgba(255, 255, 255, 0.75);
  }

  to {
    border-right-color: transparent;
  }
}

@keyframes typewriter {
  from {
    width: 0;
  }

  to {
    width: 100%;
  }
}
</style>
