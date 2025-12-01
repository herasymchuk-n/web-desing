<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

import img1 from '@/assets/illustration.svg'
import img2 from '@/assets/illustration2.svg'
import img3 from '@/assets/illustration3.svg'

const router = useRouter()
const currentSlideIndex = ref(0)

const slides = [
  {
    title: 'Meet New People',
    text: 'Select the Text tool (T) and add a new text element. Change the font style to Regular, lower the size to 10.',
    image: img1
  },
  {
    title: 'CHAT WITH EASE',
    text: 'Connect with people effortlessly using our new chat features. Stay in touch and build relationships anytime.',
    image: img2
  },
  {
    title: 'FIND YOUR MATCH',
    text: 'Discover people who share your interests and passions. Finding your perfect match has never been easier.',
    image: img3
  }
]

const currentSlide = computed(() => slides[currentSlideIndex.value] || slides[0])

const nextSlide = () => {
  if (currentSlideIndex.value < slides.length - 1) {
    currentSlideIndex.value++
  } else {
    router.push('/dating/register')
  }
}

const skip = () => {
  router.push('/dating/register')
}
</script>

<template>
  <div class="flex justify-center items-center w-full min-h-[80vh] font-sans rounded-xl overflow-hidden">
    
    <div class="w-full max-w-lg p-10 flex flex-col justify-between h-full min-h-[600px]">
      
      <div class="flex flex-col items-center text-center">
        <div class="w-4/5 max-w-xs mt-8 mb-8 h-64 flex items-center justify-center">
          <img 
            :src="currentSlide?.image" 
            :alt="currentSlide?.title" 
            class="w-full max-h-full object-contain transition-opacity duration-300" 
          />
        </div>

        <h1 class="bg-[#ff6f61] text-white py-2 px-6 rounded-md text-base font-semibold mb-5 uppercase transition-all duration-300">
          {{ currentSlide?.title }}
        </h1>

        <p class="text-xs leading-4 text-[#a5a6a4] text-center mx-5 h-12">
          {{ currentSlide?.text }}
        </p>
      </div>

      <footer class="flex justify-between items-center pt-5 pb-8 mt-auto">
        <button 
          @click="skip" 
          class="py-2 px-6 rounded-lg text-xs font-semibold bg-gray-200 text-gray-600 hover:bg-gray-300 transition cursor-pointer border-none"
        >
          SKIP
        </button>

        <div class="flex space-x-1.5">
          <span 
            v-for="(_, index) in slides" 
            :key="index"
            class="w-2 h-2 transition-colors duration-300"
            :class="currentSlideIndex === index ? 'bg-[#ff6f61]' : 'bg-[#ffd1d1]'"
          ></span>
        </div>

        <button 
          @click="nextSlide"
          class="py-2 px-6 rounded-lg text-xs font-semibold bg-[#ff6f61] text-white hover:bg-[#e05548] transition cursor-pointer border-none"
        >
          NEXT
        </button>
      </footer>

    </div>
  </div>
</template>