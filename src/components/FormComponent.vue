<template>
  <div :class="['min-h-screen p-4 md:p-8 transition-all duration-500', formWrapperClass]">
    <div class="max-w-6xl mx-auto">
      <!-- Header -->
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
            <h2 :class="['text-2xl font-bold text-gray-800 mb-8 border-l-4 pl-4', borderAccent]">Lo básico de ti</h2>
            <div class="grid md:grid-cols-2 gap-6">
              <!-- Género -->
              <div class="space-y-3">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Cómo te identificas?</label>
                <div class="space-y-2">
                  <label v-for="o in genderOptions" :key="o.value"
                    class="flex items-center p-4 rounded-2xl border-2 cursor-pointer transition-all duration-200 hover:shadow-md"
                    :class="formData.Gender === o.value ? selectedBorder : defaultBorder">
                    <input type="radio" v-model="formData.Gender" :value="o.value" class="sr-only">
                    <div class="w-4 h-4 rounded-full border-2 mr-3 flex items-center justify-center"
                      :class="formData.Gender === o.value ? selectedBorder : 'border-gray-300'">
                      <div v-if="formData.Gender === o.value" :class="['w-2 h-2 rounded-full', fillAccent]"></div>
                    </div>
                    <span class="font-medium text-gray-700">{{ o.label }}</span>
                  </label>
                  <div v-if="errors.Gender" class="text-red-500 text-sm mt-1">{{ errors.Gender }}</div>
                </div>
              </div>

              <!-- Nivel académico -->
              <div class="space-y-3">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Último grado de
                  estudio?</label>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-2">
                  <label v-for="o in academicOptions" :key="o.value"
                    class="flex items-center p-4 rounded-2xl border-2 cursor-pointer transition-all duration-200 hover:shadow-md"
                    :class="formData.Academic_Level === o.value ? selectedBorder : defaultBorder">
                    <input type="radio" v-model="formData.Academic_Level" :value="o.value" class="sr-only">
                    <div class="w-4 h-4 rounded-full border-2 mr-3 flex items-center justify-center"
                      :class="formData.Academic_Level === o.value ? selectedBorder : 'border-gray-300'">
                      <div v-if="formData.Academic_Level === o.value" :class="['w-2 h-2 rounded-full', fillAccent]">
                      </div>
                    </div>
                    <span class="font-medium text-gray-700">{{ o.label }}</span>
                  </label>
                </div>
            <div v-if="errors.Academic_Level" class="text-red-500 text-sm mt-1">{{ errors.Academic_Level }}</div>
              </div>
            </div>

            <!-- País -->
            <div class="mt-8 space-y-3 mb-3">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Desde dónde nos
                escribes?</label>
              <select v-model="formData.Country"
                class="w-full p-4 text-lg border-2 rounded-2xl focus:outline-none bg-white/50 backdrop-blur-sm"
                :class="[defaultBorder, focusAccent]">
                <option disabled value="">Elige tu país...</option>
                <option v-for="c in countries" :key="c" :value="c">{{ c }}</option>
              </select>
              <div v-if="errors.Country" class="text-red-500 text-sm mt-1">{{ errors.Country }}</div>
            </div>

            <!-- Edad -->
            <div class="space-y-3">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide mt-3">¿Cuántos años
                tienes?</label>
              <input v-model="formData.Age" type="number" min="5" max="99" placeholder="Ej. 20"
                class="w-full p-4 text-lg border-2 rounded-2xl focus:outline-none bg-white/50 backdrop-blur-sm"
                :class="[defaultBorder, focusAccent]" />
            </div>
                            <div v-if="errors.Age" class="text-red-500 text-sm mt-1">{{ errors.Age }}</div>

          </div>

          <!-- Digital -->
          <div :class="cardClass">
            <h2 :class="['text-2xl font-bold text-gray-800 mb-8 border-l-4 pl-4', borderAccentAlt]">Tu mundo digital
            </h2>
            <!-- Red social -->
            <div class="mb-8 space-y-4">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Cuál es la red social que más
                utilizas?</label>
              <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
                <label v-for="p in platforms" :key="p.value" class="relative cursor-pointer group">
                  <input type="radio" v-model="formData.Most_Used_Platform" :value="p.value" class="sr-only">
                  <div class="p-4 rounded-2xl border-2 text-center transition-all duration-200 group-hover:shadow-lg"
                    :class="formData.Most_Used_Platform === p.value ? selectedBorder : defaultBorder">
                    <div class="w-8 h-8 mx-auto mb-2" v-html="p.icon"></div>
                    <div class="text-sm font-medium text-gray-700">{{ p.label }}</div>
                  </div>
                </label>
                <div v-if="errors.Most_Used_Platform" class="text-red-500 text-sm mt-1">{{ errors.Most_Used_Platform }}
                </div>
              </div>
            </div>

            <!-- ¿Afecta el rendimiento? -->
            <div class="space-y-3 mb-3">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Las redes sociales afectan tu
                rendimiento académico?</label>
              <div class="grid grid-cols-2 gap-4">
                <label :class="formData.Affects_Academic_Performance === 'Sí' ? selectedBorder : defaultBorder"
                  class="flex items-center justify-center p-4 rounded-2xl border-2 cursor-pointer hover:shadow-md">
                  <input type="radio" value="Sí" v-model="formData.Affects_Academic_Performance" class="sr-only" />
                  <span class="font-medium text-gray-700">Sí</span>
                </label>
                <label :class="formData.Affects_Academic_Performance === 'No' ? selectedBorder : defaultBorder"
                  class="flex items-center justify-center p-4 rounded-2xl border-2 cursor-pointer hover:shadow-md">
                  <input type="radio" value="No" v-model="formData.Affects_Academic_Performance" class="sr-only" />
                  <span class="font-medium text-gray-700">No</span>
                </label>
              </div>
              <div v-if="errors.Affects_Academic_Performance" class="text-red-500 text-sm mt-1">{{
                errors.Affects_Academic_Performance }}</div>
            </div>

            <!-- Uso diario -->
            <div class="space-y-6 mb-4">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Cuánto tiempo pasas conectado
                en esta red social?</label>
              <div :class="['p-8 rounded-3xl', gradientSlider]">
                <div class="text-center mb-6">
                  <div class="inline-flex items-baseline space-x-2">
                    <span :class="['text-5xl font-black', textAccent]">{{ formData.Avg_Daily_Usage_Hours }}</span>
                    <span class="text-xl text-gray-600">horas al día</span>
                  </div>
                </div>
                <input v-model="formData.Avg_Daily_Usage_Hours" type="range" min="0" max="10" step="0.5"
                  class="w-full h-2 rounded-full appearance-none cursor-pointer" :class="sliderClass" />
              </div>
              <div v-if="errors.Avg_Daily_Usage_Hours" class="text-red-500 text-sm mt-1">{{ errors.Avg_Daily_Usage_Hours
                }}</div>
            </div>

            <!-- Segundo Slider-->
            <div class="space-y-6">
              <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Con qué frecuencia tienes
                conflictos por redes sociales?</label>
              <div :class="['p-8 rounded-3xl', gradientSlider]">
                <div class="text-center mb-6">
                  <div class="inline-flex items-center justify-center space-x-2">
                    <span :class="['text-5xl font-black', textAccent]">{{ formData.Conflicts_Over_Social_Media }}</span>
                    <span class="text-xl text-gray-600" v-if="formData.Conflicts_Over_Social_Media == 1">vez por
                      semana</span>
                    <span class="text-xl text-gray-600" v-else>veces por semana</span>
                  </div>
                  <div class="text-sm text-gray-500 mt-2">{{ getConflictLevel(formData.Conflicts_Over_Social_Media) }}
                  </div>
                </div>
                <input v-model="formData.Conflicts_Over_Social_Media" type="range" min="0" max="5" step="1"
                  class="w-full h-2 rounded-full appearance-none cursor-pointer" :class="sliderClass" />
                <div class="justify-between mt-2 text-sm text-gray-500 hidden sm:flex">
                  <span>Nunca</span>
                  <span>Rara vez</span>
                  <span>A veces</span>
                  <span>Frecuente</span>
                  <span>Muy frecuente</span>
                </div>
              </div>
              <div v-if="errors.Conflicts_Over_Social_Media" class="text-red-500 text-sm mt-1">{{
              errors.Conflicts_Over_Social_Media }}</div>
            </div>

          </div>

          <!-- Personal -->
          <div :class="cardClass">
            <h2 :class="['text-2xl font-bold text-gray-800 mb-8 border-l-4 pl-4', borderAccent]">Tu lado humano</h2>
            <div class="grid md:grid-cols-2 gap-8">
              <!-- Relación -->
              <div class="space-y-4">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Situación sentimental
                  actual?</label>
                <div class="space-y-3">
                  <label v-for="s in relationshipOptions" :key="s.value"
                    class="flex items-center p-4 rounded-2xl border-2 cursor-pointer hover:shadow-md"
                    :class="formData.Relationship_Status === s.value ? selectedBorder : defaultBorder">
                    <input type="radio" v-model="formData.Relationship_Status" :value="s.value" class="sr-only">
                    <span class="font-medium text-gray-700">{{ s.label }}</span>
                  </label>
                </div>
                <div v-if="errors.Relationship_Status" class="text-red-500 text-sm mt-1">{{ errors.Relationship_Status
                  }}</div>
              </div>

              <!-- Sueño -->
              <div class="space-y-6">
                <label class="text-sm font-semibold text-gray-700 uppercase tracking-wide">¿Cuántas horas duermes por
                  noche realmente?</label>
                <div :class="['p-6 rounded-3xl', gradientSlider]">
                  <div class="text-center mb-4">
                    <div class="inline-flex items-baseline space-x-2">
                      <span :class="['text-4xl font-black', textAccent]">{{ formData.Sleep_Hours_Per_Night }}</span>
                      <span class="text-lg text-gray-600">horas</span>
                    </div>
                    <div class="text-sm text-gray-500 mt-1">{{ getSleepComment(formData.Sleep_Hours_Per_Night) }}</div>
                  </div>
                  <input v-model="formData.Sleep_Hours_Per_Night" type="range" min="0" max="10" step="0.5"
                    class="w-full h-2 rounded-full appearance-none cursor-pointer" :class="sliderClass" />
                </div>
              </div>
              <div v-if="errors.Sleep_Hours_Per_Night" class="text-red-500 text-sm mt-1">{{ errors.Sleep_Hours_Per_Night
                }}</div>
            </div>
          </div>

          <!-- Botón -->
          <div class="text-center mt-4 sm:mb-0 mb-4">
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
  <!-- Modal de éxito -->
<transition
  enter-active-class="transition duration-300 ease-out"
  enter-from-class="opacity-0 scale-90"
  enter-to-class="opacity-100 scale-100"
  leave-active-class="transition duration-200 ease-in"
  leave-from-class="opacity-100 scale-100"
  leave-to-class="opacity-0 scale-90"
>
  <div
    v-if="showSuccessModal"
    class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm"
  >
    <div
      class="bg-white rounded-3xl p-8 shadow-xl max-w-md w-full text-center border-t-4 transform transition duration-300 hover:scale-105 hover:shadow-2xl"
      :class="borderAccent"
    >
      <h2 class="text-2xl font-bold text-gray-800 mb-4">¡Gracias!</h2>
      <p class="text-gray-600 mb-6">Tus datos se guardaron correctamente.</p>
      <button
        @click="showSuccessModal = false"
        class="px-6 py-3 font-semibold rounded-full text-white transition-all duration-300 hover:scale-105 hover:shadow-xl"
        :class="buttonGradient"
      >
        Cerrar
      </button>
    </div>
  </div>
</transition>

</template>

<script lang="ts" setup>
import { Form } from "@/composables/Form"

const {
  formData,
  errors,
  genderOptions,
  academicOptions,
  relationshipOptions,
  countries,
  platforms,
  getConflictLevel,
  formWrapperClass,
  titleGradient,
  accentText,
  borderAccent,
  borderAccentAlt,
  cardClass,
  selectedBorder,
  defaultBorder,
  focusAccent,
  fillAccent,
  bubbleAccent,
  gradientSlider,
  textAccent,
  sliderClass,
  buttonGradient,
  getSleepComment,
  submitForm,
  showSuccessModal
} = Form()
</script>
