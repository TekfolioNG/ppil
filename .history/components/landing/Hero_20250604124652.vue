<template>
  <main class="relative w-screen h-screen overflow-hidden">
    <!-- Slides wrapper - full width with edge-to-edge coverage -->
    <div class="absolute inset-0 w-screen h-full overflow-hidden z-0">
      <transition-group :name="transitions[currentSlide]" tag="div" class="h-full">
        <div v-for="(slide, index) in slides" :key="index" v-show="currentSlide === index"
          class="absolute inset-0 w-screen h-full">
          <img :src="slide.image" :alt="slide.alt" class="w-full h-full object-cover object-center" />
          <!-- Gradient overlay -->
          <div class="absolute inset-0 bg-gradient-to-b from-black/40 via-black/20 to-black/50" />

        </div>
      </transition-group>
    </div>

    <!-- Content overlay - positioned closer to bottom and shifted left -->
    <div class="relative z-20 w-full h-full flex flex-col px-6 md:pl-16 lg:pl-24 xl:pl-32">
      <div class="flex flex-col mt-auto mb-16 md:mb-20 lg:mb-28 max-w-3xl mx-auto md:mx-0">
        <transition :name="textTransitions[currentSlide]" mode="out-in">
          <h1 :key="'title-' + currentSlide"
            class="hero-heading font-heading text-4xl md:text-5xl lg:text-6xl text-white font-black tracking-wider-custom leading-tight">
            {{ slides[currentSlide].title }}
          </h1>
        </transition>
        <transition :name="textTransitions[currentSlide]" mode="out-in">
          <p :key="'desc-' + currentSlide"
            class="mt-4 text-lg md:text-xl text-gray-100 max-w-2xl font-light leading-relaxed">
            {{ slides[currentSlide].description }}
          </p>
        </transition>
        <div class="mt-8 flex flex-wrap gap-4 justify-center md:justify-start">
          <NuxtLink :to="slides[currentSlide].primaryLink"
            class="px-6 py-3 border-2 text-white hover:bg-yellow-500 hover:text-black font-medium transition-all duration-300 text-lg transform hover:scale-105">
            {{ slides[currentSlide].primaryText }}
          </NuxtLink>
          <NuxtLink :to="slides[currentSlide].secondaryLink"
            class="px-6 py-3 border-2 text-white hover:bg-white hover:text-black transition-all duration-300 font-medium text-lg transform hover:scale-105">
            {{ slides[currentSlide].secondaryText }}
          </NuxtLink>
        </div>
      </div>
    </div>

    <!-- Slide navigation -->
    <div class="absolute bottom-8 left-0 right-0 z-30 flex justify-center gap-2">
      <button v-for="(_, index) in slides" :key="index" @click="setSlide(index)"
        class="w-12 h-1.5 transition-all duration-300 rounded-full"
        :class="currentSlide === index ? 'bg-yellow' : 'bg-white/40 hover:bg-white/60'"
        :aria-label="`Go to slide ${index + 1}`">
      </button>
    </div>

    <!-- Progress bar -->
    <div class="absolute bottom-0 left-0 right-0 z-30 h-1 bg-white/20">
      <div class="bg-yellow h-full transition-all duration-300 ease-linear" :style="{ width: `${progress}%` }"></div>
    </div>
  </main>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';

// Import images
import ppil1 from '/assets/img/PPIL1.png';
import ppil2 from '/assets/img/PPIL2.jpg';
import ppil3 from '/assets/img/PPIL3.jpg';

const SLIDE_DURATION = 8000; // 8 seconds per slide
const slides = [
  {
    image: ppil1,
    alt: 'PPIL Construction Site',
    title: 'Smart infrastructure. Premium execution.',
    description: 'We design, build, and maintain high-impact projects — combining deep technical know-how with a future-ready mindset for real results.',
    primaryLink: '/who-we-are',
    primaryText: 'Who We Are',
    secondaryLink: '/what-we-do',
    secondaryText: 'What We Do'
  },
  {
    image: ppil3,
    alt: 'PPIL Infrastructure Project',
    title: 'We consistently deliver precision & integrity.',
    description: 'At PPIL, we bring vision to life through expertly managed design, construction, and infrastructure solutions.',
    primaryLink: '/our-work',
    primaryText: 'Our Work',
    secondaryLink: '/our-team',
    secondaryText: 'Our Team'
  },
  {
    image: ppil2,
    alt: 'PPIL Commercial Building',
    title: 'Engineering projects. Building relationships.',
    description: 'PPIL is your trusted partner for sustainable construction, project management, and maintenance, shaping environments that last generations.',
    primaryLink: '/who-we-are',
    primaryText: 'Why PPIL',
    secondaryLink: '/contact',
    secondaryText: 'Contact Us'
  }
]

const transitions = ['fade', 'slide-up', 'zoom']
const textTransitions = ['fade', 'slide-left', 'slide-up']

const currentSlide = ref(0)
const progress = ref(0)
let timer = null
let progressTimer = null

const setSlide = (index) => {
  currentSlide.value = index
  resetProgress()
}

const resetProgress = () => {
  progress.value = 0
  if (progressTimer) {
    clearInterval(progressTimer)
  }

  progressTimer = setInterval(() => {
    progress.value += (100 / (SLIDE_DURATION / 100))
    if (progress.value >= 100) {
      progress.value = 0
    }
  }, 100)
}

onMounted(() => {
  timer = setInterval(() => {
    currentSlide.value = (currentSlide.value + 1) % slides.length
    resetProgress()
  }, SLIDE_DURATION)

  resetProgress()
})

onBeforeUnmount(() => {
  if (timer) clearInterval(timer)
  if (progressTimer) clearInterval(progressTimer)
})
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-up-enter-active,
.slide-up-leave-active {
  transition: opacity 1.2s ease, transform 1.2s ease;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

.slide-up-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}

.zoom-enter-active,
.zoom-leave-active {
  transition: opacity 1.5s ease, transform 1.5s ease;
}

.zoom-enter-from {
  opacity: 0;
  transform: scale(1.1);
}

.zoom-leave-to {
  opacity: 0;
  transform: scale(0.95);
}

.slide-left-enter-active,
.slide-left-leave-active {
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(20px);
}

.slide-left-leave-to {
  opacity: 0;
  transform: translateX(-20px);
}

.font-heading,
.hero-heading {
  font-family: "Noto Sans", sans-serif;
  font-weight: 700;
  line-height: 1.05;
  letter-spacing: 0.01em;
  text-shadow: 0 2px 6px rgba(0, 0, 0, 0.5);
  -webkit-text-stroke: 0.5px white;
}

.hero-heading {
  text-shadow:
    0 2px 6px rgba(0, 0, 0, 0.5),
    0 0 1px #fff,
    0 0 1px #fff;
}

.w-screen {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
}

.hover\:bg-transparent:hover {
  background-color: transparent;
}

@media (max-width: 767px) {
  .hero-heading {
    text-align: center;
  }

  p {
    text-align: center;
  }
}
</style>