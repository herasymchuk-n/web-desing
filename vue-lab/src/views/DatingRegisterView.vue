<script setup lang="ts">
import { ref } from 'vue'

const isLoginMode = ref(false)

const setLogin = () => {
  isLoginMode.value = true
}

const setRegister = () => {
  isLoginMode.value = false
}
</script>

<template>
  <div class="bg-[#ff6f61] flex justify-center items-center w-full min-h-[80vh] font-sans rounded-xl overflow-hidden">

    <div class="w-full max-w-lg p-8 md:p-10 flex flex-col items-center text-center gap-5">

      <div class="mb-4">
        <div class="bg-white text-[#ff6f61] rounded-full w-24 h-24 flex justify-center items-center mb-2 font-bold text-[50px] mx-auto select-none">
            ❤️
        </div>
        <h1 class="text-white text-4xl font-extrabold m-0 tracking-widest">FATED</h1>
      </div>

      <div class="flex w-full max-w-xs mb-6">
        
        <button 
          @click="setLogin"
          class="flex-1 py-2 border-2 border-white text-sm font-semibold cursor-pointer rounded-l-lg border-r-0 flex justify-center items-center transition"
          :class="isLoginMode 
            ? 'bg-white text-[#ff6f61]'  
            : 'bg-[#ff857a] text-white hover:bg-[#ff958b]'"
        >
            LOGIN
        </button>

        <button 
          @click="setRegister"
          class="flex-1 py-2 border-2 border-white text-sm font-semibold cursor-pointer rounded-r-lg transition"
          :class="!isLoginMode 
            ? 'bg-white text-[#ff6f61]' 
            : 'bg-[#ff857a] text-white hover:bg-[#ff958b]'"
        >
            REGISTER
        </button>
      </div>

      <form class="flex flex-col w-full max-w-sm gap-3" @submit.prevent>
        
        <input type="text" placeholder="user name"
            class="p-4 border-none rounded-lg text-sm text-center text-gray-700 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-[#ff857a]" />
        
        <input type="password" placeholder="password"
            class="p-4 border-none rounded-lg text-sm text-center text-gray-700 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-[#ff857a]" />
        
        <input v-if="!isLoginMode" type="email" placeholder="email"
            class="p-4 border-none rounded-lg text-sm text-center text-gray-700 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-[#ff857a]" />

        <p class="text-white text-xs font-medium ml-auto mt-1 mb-2 cursor-pointer hover:text-gray-100">FORGOT PASSWORD?</p>
        
        <button type="submit"
            class="p-4 border-none rounded-lg bg-white text-[#ff6f61] text-base font-bold cursor-pointer mt-1 hover:bg-gray-100 transition shadow-lg">
            {{ isLoginMode ? 'LOGIN' : 'REGISTER' }}
        </button>
      </form>

      <p class="text-white text-sm font-medium mt-4">
        {{ isLoginMode ? "DON'T HAVE AN ACCOUNT?" : "ALREADY HAVE AN ACCOUNT?" }}
        
        <span 
          @click="isLoginMode = !isLoginMode"
          class="text-white font-bold cursor-pointer hover:underline ml-1"
        >
          {{ isLoginMode ? 'REGISTER' : 'LOGIN' }}
        </span>
      </p>
    </div>
  </div>
</template>