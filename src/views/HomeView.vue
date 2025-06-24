<template>
  <div :class="['min-h-screen p-4 md:p-8 transition-all duration-500', formWrapperClass]">
    <div class="max-w-4xl mx-auto">

      <!-- Header creativo -->
      <div class="text-center mb-12 relative">
        <div
          class="absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-4 w-32 h-32 rounded-full opacity-20 blur-xl"
          :class="bubbleAccent" />
        <h1 class="text-4xl md:text-5xl font-black text-gray-800 mb-3 relative z-10">
          <span :class="titleGradient" class="bg-clip-text text-transparent">Cuéntanos</span><br>
          <span class="text-gray-700">acerca de ti</span>
        </h1>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto leading-relaxed">
          Una encuesta diferente sobre tus hábitos como estudiante.
          <span :class="['font-medium', accentText]">Sé honesto, sé tú mismo.</span>
        </p>
      </div>

      <!-- Formulario -->
      <div class="relative">
        <div class="absolute -top-8 -right-8 w-64 h-64 rounded-full opacity-10 blur-2xl" :class="bubbleAccent" />
        <div class="absolute top-1/2 -left-12 w-48 h-48 rounded-full opacity-10 blur-2xl" :class="bubbleAccent" />

        <form @submit.prevent="submitForm" class="relative z-10 space-y-8">
          <!-- Básico -->
          <div :class="cardClass">
            <h2 :class="['text-2xl font-bold text-gray-800 mb-8 border-l-4 pl-4', borderAccent]">
              Lo básico de ti
            </h2>
            <div class="grid md:grid-cols-2 gap-6">
              <!-- Género -->
              <div class="space-y-3">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">
                  ¿Cómo te identificas?
                </label>
                <div class="space-y-2">
                  <label v-for="o in genderOptions" :key="o.value"
                    class="flex items-center p-4 rounded-2xl border-2 cursor-pointer transition-all duration-200 hover:shadow-md"
                    :class="formData.gender === o.value ? selectedBorder : defaultBorder">
                    <input type="radio" v-model="formData.gender" :value="o.value" class="sr-only">
                    <div class="w-4 h-4 rounded-full border-2 mr-3 flex items-center justify-center"
                      :class="formData.gender === o.value ? selectedBorder : 'border-gray-300'">
                      <div v-if="formData.gender === o.value" :class="['w-2 h-2 rounded-full', fillAccent]"></div>
                    </div>
                    <span class="font-medium text-gray-700">{{ o.label }}</span>
                  </label>
                </div>
              </div>

              <!-- Nivel académico -->
              <div class="space-y-3">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">
                  ¿En qué nivel estás?
                </label>
                <div class="space-y-2">
                  <label v-for="o in academicOptions" :key="o.value"
                    class="flex items-center p-4 rounded-2xl border-2 cursor-pointer transition-all duration-200 hover:shadow-md"
                    :class="formData.academicLevel === o.value ? selectedBorder : defaultBorder">
                    <input type="radio" v-model="formData.academicLevel" :value="o.value" class="sr-only">
                    <div class="w-4 h-4 rounded-full border-2 mr-3 flex items-center justify-center"
                      :class="formData.academicLevel === o.value ? selectedBorder : 'border-gray-300'">
                      <div v-if="formData.academicLevel === o.value" :class="['w-2 h-2 rounded-full', fillAccent]">
                      </div>
                    </div>
                    <span class="font-medium text-gray-700">{{ o.label }}</span>
                  </label>
                </div>
              </div>
            </div>
            <!-- País -->
            <div class="mt-8 space-y-3">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">
                ¿Desde dónde nos escribes?
              </label>
              <select v-model="formData.country"
                class="w-full p-4 text-lg border-2 rounded-2xl focus:outline-none transition-colors duration-200 bg-white/50 backdrop-blur-sm"
                :class="[defaultBorder, focusAccent]">
                <option disabled value="">Elige tu país...</option>
                <option v-for="c in countries" :key="c" :value="c">{{ c }}</option>
              </select>
            </div>

            <!-- Edad -->
            <div class="space-y-3">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide mt-3">
                ¿Cuántos años tienes?
              </label>
              <input v-model="formData.age" type="number" min="5" max="99" placeholder="Ej. 20"
                class="w-full p-4 text-lg border-2 rounded-2xl focus:outline-none transition-colors duration-200 bg-white/50 backdrop-blur-sm"
                :class="[defaultBorder, focusAccent]" />
            </div>

          </div>

          <!-- Digital -->
          <div :class="cardClass">
            <h2 :class="['text-2xl font-bold text-gray-800 mb-8 border-l-4 pl-4', borderAccentAlt]">
              Tu mundo digital
            </h2>
            <!-- Redes -->
            <div class="mb-8 space-y-4">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">
                ¿Cuál es la red social que más utilizas?
              </label>
              <div class="grid grid-cols-2 md:grid-cols-5 gap-3">
                <label v-for="p in platforms" :key="p.value" class="relative cursor-pointer group">
                  <input type="radio" v-model="formData.platform" :value="p.value" class="sr-only">
                  <div class="p-4 rounded-2xl border-2 text-center transition-all duration-200 group-hover:shadow-lg"
                    :class="formData.platform === p.value
                      ? selectedBorder
                      : defaultBorder">
                    <div class="w-8 h-8 mx-auto mb-2" v-html="p.icon"></div>
                    <div class="text-sm font-medium text-gray-700">{{ p.label }}</div>
                  </div>
                </label>
              </div>
            </div>
            <!-- Uso diario -->
            <div class="space-y-6">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">
                ¿Cuánto tiempo pasas conectado?
              </label>
              <div :class="['p-8 rounded-3xl', gradientSlider]">
                <div class="text-center mb-6">
                  <div class="inline-flex items-baseline space-x-2">
                    <span :class="['text-5xl font-black', textAccent]">{{ formData.dailyUsageHours }}</span>
                    <span class="text-xl text-gray-600">horas al día</span>
                  </div>
                </div>
                <input v-model="formData.dailyUsageHours" type="range" min="0" max="10" step="0.5"
                  class="w-full h-2 rounded-full appearance-none cursor-pointer" :class="sliderClass" />
              </div>
            </div>
          </div>

          <!-- Personal -->
          <div :class="cardClass">
            <h2 :class="['text-2xl font-bold text-gray-800 mb-8 border-l-4 pl-4', borderAccent]">
              Tu lado humano
            </h2>
            <div class="grid md:grid-cols-2 gap-8">
              <!-- Relación -->
              <div class="space-y-4">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">
                  ¿Cómo está tu corazón?
                </label>
                <div class="space-y-3">
                  <label v-for="s in relationshipOptions" :key="s.value"
                    class="flex items-center p-4 rounded-2xl border-2 cursor-pointer transition-all duration-200 hover:shadow-md"
                    :class="formData.relationshipStatus === s.value ? selectedBorder : defaultBorder">
                    <input type="radio" v-model="formData.relationshipStatus" :value="s.value" class="sr-only">
                    <span class="font-medium text-gray-700">{{ s.label }}</span>
                  </label>
                </div>
              </div>
              <!-- Sueño -->
              <div class="space-y-6">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">
                  ¿Cuánto duermes realmente?
                </label>
                <div :class="['p-6 rounded-3xl', gradientSlider]">
                  <div class="text-center mb-4">
                    <div class="inline-flex items-baseline space-x-2">
                      <span :class="['text-4xl font-black', textAccent]">{{ formData.sleepHours }}</span>
                      <span class="text-lg text-gray-600">horas</span>
                    </div>
                    <div class="text-sm text-gray-500 mt-1">{{ getSleepComment(formData.sleepHours) }}</div>
                  </div>
                  <input v-model="formData.sleepHours" type="range" min="0" max="10" step="0.5"
                    class="w-full h-2 rounded-full appearance-none cursor-pointer" :class="sliderClass" />
                </div>
              </div>
            </div>
          </div>

          <!-- Envío -->
          <div class="text-center pt-8">
            <button type="submit"
              class="cursor-pointer group relative px-12 py-4 text-white font-bold text-lg rounded-full shadow-xl hover:shadow-2xl transform hover:scale-105 transition-all duration-300 overflow-hidden"
              :class="buttonGradient">
              <span class="relative z-10">Enviar Formulario</span>
              <div class="absolute inset-0 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                :class="buttonGradient"></div>
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const formData = ref({
  gender: '',
  academicLevel: '',
  country: '',
  platform: '',
  dailyUsageHours: 3,
  relationshipStatus: '',
  sleepHours: 7,
  academicImpact: 0,
  mentalHealth: 0,
  conflicts: 0,
  addictionLevel: 0.,
  age: null,

})

const genderOptions = [{ value: 'Masculino', label: 'Masculino' }, { value: 'Femenino', label: 'Femenino' }]
const academicOptions = [{ value: 'Preparatoria', label: 'Preparatoria' }, { value: 'Licenciatura', label: 'Licenciatura' }, { value: 'Posgrado', label: 'Posgrado' }]
const countries = ['México', 'Colombia', 'Chile', 'Perú', 'Argentina', 'Ecuador', 'España', 'USA']
const platforms = [
  {
    value: 'Instagram',
    label: 'Instagram',
    icon: `
      <svg viewBox="0 0 24 24" fill="currentColor" class="w-full h-full text-pink-500">
      <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
    </svg>
    `,
  },
  {
    value: 'Facebook',
    label: 'Facebook',
    icon: `
      <svg viewBox="0 0 24 24" fill="currentColor" class="w-full h-full text-blue-600">
      <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
    </svg>
    `,
  },
  {
    value: 'TikTok',
    label: 'TikTok',
    icon: `
      <svg viewBox="0 0 24 24" fill="currentColor" class="w-full h-full text-gray-800">
      <path d="M12.525.02c1.31-.02 2.61-.01 3.91-.02.08 1.53.63 3.09 1.75 4.17 1.12 1.11 2.7 1.62 4.24 1.79v4.03c-1.44-.05-2.89-.35-4.2-.97-.57-.26-1.1-.59-1.62-.93-.01 2.92.01 5.84-.02 8.75-.08 1.4-.54 2.79-1.35 3.94-1.31 1.92-3.58 3.17-5.91 3.21-1.43.08-2.86-.31-4.08-1.03-2.02-1.19-3.44-3.37-3.65-5.71-.02-.5-.03-1-.01-1.49.18-1.9 1.12-3.72 2.58-4.96 1.66-1.44 3.98-2.13 6.15-1.72.02 1.48-.04 2.96-.04 4.44-.99-.32-2.15-.23-3.02.37-.63.41-1.11 1.04-1.36 1.75-.21.51-.15 1.07-.14 1.61.24 1.64 1.82 3.02 3.5 2.87 1.12-.01 2.19-.66 2.77-1.61.19-.33.4-.67.41-1.06.1-1.79.06-3.57.07-5.36.01-4.03-.01-8.05.02-12.07z"/>
    </svg>
    `,
  },
  {
    value: 'Twitter',
    label: 'Twitter',
    icon: `
      <svg viewBox="0 0 24 24" fill="currentColor" class="w-full h-full text-sky-500">
      <path d="M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"/>
    </svg>
    `,
  },
  {
    value: 'YouTube',
    label: 'YouTube',
    icon: `
      <svg viewBox="0 0 24 24" fill="currentColor" class="w-full h-full text-red-600">
      <path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
    </svg>
    `,
  },
  {
  value: 'LinkedIn',
  label: 'LinkedIn',
  icon: `
    <svg viewBox="0 0 24 24" class="w-full h-full text-blue-600" xmlns="http://www.w3.org/2000/svg" fill="currentColor">
      <path d="M4.98 3.5a2.5 2.5 0 1 1-4.96 0 2.5 2.5 0 0 1 4.96 0ZM.5 8.5h4.96v14H.5v-14ZM8.5 8.5H13v2h.06c.63-1.2 2.18-2.46 4.44-2.46 4.75 0 5.63 3.13 5.63 7.2V22.5h-4.96v-6.5c0-1.55 0-3.53-2.15-3.53s-2.49 1.68-2.49 3.42v6.61H8.5v-14Z"/>
    </svg>
  `,
},

{
  value: 'WhatsApp',
  label: 'WhatsApp',
  icon: `
    <svg viewBox="0 0 32 32" class="w-full h-full text-green-500" xmlns="http://www.w3.org/2000/svg" fill="currentColor">
      <path d="M16.005 2.667c-7.364 0-13.338 5.974-13.338 13.338 0 2.352.621 4.65 1.797 6.667L2.667 29.333l6.805-1.797c1.933 1.13 4.117 1.732 6.533 1.732 7.364 0 13.333-5.969 13.333-13.333S23.369 2.667 16.005 2.667Zm0 24c-1.938 0-3.83-.528-5.467-1.528l-.391-.234-4.008 1.063 1.063-3.984-.257-.406a10.578 10.578 0 0 1-1.617-5.546c0-5.84 4.761-10.6 10.6-10.6s10.6 4.761 10.6 10.6-4.761 10.6-10.6 10.6Zm5.406-7.873c-.297-.148-1.75-.867-2.023-.967s-.469-.148-.664.148-.762.967-.933 1.166c-.171.195-.336.222-.633.074s-1.238-.457-2.355-1.457c-.87-.777-1.457-1.735-1.63-2.027-.172-.296-.018-.457.13-.605.133-.133.297-.336.445-.504.148-.171.196-.296.297-.495.099-.198.05-.371-.025-.52-.074-.148-.664-1.6-.91-2.192-.24-.576-.481-.498-.664-.508l-.566-.01c-.197 0-.519.074-.79.37s-1.036 1.012-1.036 2.467 1.06 2.857 1.209 3.054c.148.198 2.093 3.195 5.074 4.48.709.305 1.263.487 1.694.623.712.227 1.36.195 1.872.118.571-.085 1.75-.715 1.997-1.406.247-.69.247-1.28.173-1.406-.074-.124-.271-.198-.57-.347Z"/>
    </svg>
  `,
},

]

const relationshipOptions = [
  { value: 'Soltero/a', label: 'Soltero/a' },
  { value: 'En una relación', label: 'En una relación' },
  { value: 'Es complicado', label: 'Es complicado' }
]

const isFeminine = computed(() => formData.value.gender === 'Femenino')
const formWrapperClass = computed(() => isFeminine.value
  ? 'bg-gradient-to-br from-pink-100 via-rose-100 to-amber-50'
  : 'bg-gradient-to-br from-blue-100 via-indigo-100 to-cyan-50')
const titleGradient = computed(() => isFeminine.value
  ? 'bg-gradient-to-r from-pink-500 to-rose-400'
  : 'bg-gradient-to-r from-blue-700 to-indigo-600')
const accentText = computed(() => isFeminine.value ? 'text-pink-500' : 'text-blue-700')
const borderAccent = computed(() => isFeminine.value ? 'border-pink-400' : 'border-blue-400')
const borderAccentAlt = computed(() => isFeminine.value ? 'border-rose-400' : 'border-indigo-400')
const cardClass = computed(() =>
  'bg-white/80 backdrop-blur-sm rounded-3xl p-8 shadow-xl border border-white/50 transform transition-transform duration-300')
const selectedBorder = computed(() => isFeminine.value ? 'border-pink-400 bg-pink-50' : 'border-blue-400 bg-blue-50')
const defaultBorder = 'border-gray-200 hover:border-opacity-60'
const focusAccent = computed(() => isFeminine.value ? 'focus:border-pink-400' : 'focus:border-cyan-400')
const fillAccent = computed(() => isFeminine.value ? 'bg-pink-400' : 'bg-blue-400')
const bubbleAccent = computed(() => isFeminine.value ? 'bg-gradient-to-r from-pink-200 to-rose-300' : 'bg-gradient-to-r from-blue-200 to-indigo-200')
const gradientSlider = computed(() => isFeminine.value ? 'bg-gradient-to-r from-pink-100 to-rose-100' : 'bg-gradient-to-r from-indigo-100 to-blue-100')
const textAccent = computed(() => isFeminine.value ? 'text-pink-600' : 'text-indigo-600')
const sliderClass = computed(() => isFeminine.value ? 'bg-rose-200' : 'bg-white slider-unique')
const buttonGradient = computed(() => isFeminine.value
  ? 'bg-gradient-to-r from-pink-400 via-rose-400 to-amber-400'
  : 'bg-gradient-to-r from-blue-500 via-indigo-500 to-cyan-500')

const getSleepComment = (h: number) => {
  if (h < 4) return 'Eso no es saludable 😴'
  if (h < 6) return 'Muy poco descanso'
  if (h < 8) return 'Podría ser mejor'
  if (h < 9) return 'Perfecto balance'
  return 'Eres un dormilón 😊'
}

const submitForm = () => {
  formData.value.academicImpact = Math.random() * 10
  formData.value.mentalHealth = Math.random() * 10
  formData.value.conflicts = Math.random() * 10
  formData.value.addictionLevel = Math.random() * 10
  console.log('Enviado:', formData.value)
  alert('¡Perfecto! Tus datos han sido registrados 🎉')
}
</script>
