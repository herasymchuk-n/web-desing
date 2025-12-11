<script setup lang="ts">
import { ref, reactive } from 'vue'

const isLoginMode = ref(true)

const formState = reactive({
  username: '',
  password: '',
  email: ''
})

const errors = reactive({
  username: '',
  password: '',
  email: ''
})

const setLogin = () => {
  isLoginMode.value = true
  clearErrors()
}

const setRegister = () => {
  isLoginMode.value = false
  clearErrors()
}

const clearErrors = () => {
  errors.username = ''
  errors.password = ''
  errors.email = ''
}

const validateField = (field: 'username' | 'password' | 'email') => {

  if (field === 'username') {
    errors.username = !formState.username ? "User name is required" : ""
  }

  if (field === 'password') {
    if (!formState.password) {
      errors.password = "Password is required"
    } else if (formState.password.length < 8) {
      errors.password = "Password must be at least 8 chars"
    } else if (!/[a-zA-Z]/.test(formState.password)) {
      errors.password = "Password must contain at least one letter"
    } else {
      errors.password = ""
    }
  }

  if (field === 'email' && !isLoginMode.value) {
    if (!formState.email) {
      errors.email = "Email is required"
    } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formState.email)) {
      errors.email = "Invalid email format"
    } else {
      errors.email = ""
    }
  }
}

const validateForm = () => {
  validateField('username')
  validateField('password')
  if (!isLoginMode.value) validateField('email')

  return !(errors.username || errors.password || errors.email)
}

const submitForm = () => {
  if (validateForm()) {
    
    if (isLoginMode.value) {
      console.log(`LOGIN DATA -> Username: ${formState.username} | Password: ${formState.password}`)
    } else {
      console.log(`REGISTER DATA -> Username: ${formState.username} | Password: ${formState.password} | Email: ${formState.email}`)
    }

    alert('Form sent! Check console.')
  } else {
    console.log('Validation failed')
  }
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

      <form class="flex flex-col w-full max-w-sm gap-3" @submit.prevent="submitForm">
        
        <div class="w-full">
          <input 
            type="text" 
            placeholder="user name"
            v-model="formState.username"
            @input="validateField('username')" 
            class="w-full p-4 border-none rounded-lg text-sm text-center text-gray-700 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-[#ff857a]" 
            :class="{'ring-2 ring-red-500': errors.username}"
          />
          <span v-if="errors.username" class="text-white text-xs text-left mt-1 block pl-1 transition-all duration-200">
            {{ errors.username }}
          </span>
        </div>
        
        <div class="w-full">
          <input 
            type="password" 
            placeholder="password"
            v-model="formState.password"
            @input="validateField('password')"
            class="w-full p-4 border-none rounded-lg text-sm text-center text-gray-700 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-[#ff857a]" 
            :class="{'ring-2 ring-red-500': errors.password}"
          />
          <span v-if="errors.password" class="text-white text-xs text-left mt-1 block pl-1 transition-all duration-200">
            {{ errors.password }}
          </span>
        </div>
        
        <div class="w-full" v-if="!isLoginMode">
          <input 
            type="email" 
            placeholder="email"
            v-model="formState.email"
            @input="validateField('email')"
            class="w-full p-4 border-none rounded-lg text-sm text-center text-gray-700 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-[#ff857a]" 
            :class="{'ring-2 ring-red-500': errors.email}"
          />
          <span v-if="errors.email" class="text-white text-xs text-left mt-1 block pl-1 transition-all duration-200">
            {{ errors.email }}
          </span>
        </div>

        <p class="text-white text-xs font-medium ml-auto mt-1 mb-2 cursor-pointer hover:text-gray-100">FORGOT PASSWORD?</p>
        
        <button type="submit"
            class="w-full p-4 border-none rounded-lg bg-white text-[#ff6f61] text-base font-bold cursor-pointer mt-1 hover:bg-gray-100 transition shadow-lg">
            {{ isLoginMode ? 'LOGIN' : 'REGISTER' }}
        </button>
      </form>

      <p class="text-white text-sm font-medium mt-4">
        {{ isLoginMode ? "DON'T HAVE AN ACCOUNT?" : "ALREADY HAVE AN ACCOUNT?" }}
        
        <span 
          @click="isLoginMode = !isLoginMode; clearErrors()"
          class="text-white font-bold cursor-pointer hover:underline ml-1"
        >
          {{ isLoginMode ? 'REGISTER' : 'LOGIN' }}
        </span>
      </p>
    </div>
  </div>
</template>