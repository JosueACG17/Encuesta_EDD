<template>
  <div class="min-h-screen bg-gray-50 py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl p-6">
      <h1 class="text-2xl font-bold text-gray-800 mb-6">Encuesta de Hábitos Estudiantiles</h1>

      <form @submit.prevent="submitForm" class="space-y-6">
        <!-- Información básica -->
        <div class="space-y-4">
          <h2 class="text-lg font-medium text-gray-700">Información Básica</h2>

          <!-- Género -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Género</label>
            <select v-model="formData.gender" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md border">
              <option value="" disabled selected>Selecciona tu género</option>
              <option value="Masculino">Masculino</option>
              <option value="Femenino">Femenino</option>

            </select>
          </div>

          <!-- Nivel académico -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Nivel Académico</label>
            <select v-model="formData.academicLevel" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md border">
              <option value="" disabled selected>Selecciona tu nivel académico</option>
              <option value="Preparatoria">Preparatoria</option>
              <option value="Licenciatura">Licenciatura</option>
              <option value="Posgrado">Posgrado</option>
            </select>
          </div>

          <!-- País -->
<div>
  <label class="block text-sm font-medium text-gray-700 mb-1">País</label>
  <select v-model="formData.country" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md border">
    <option value="" disabled selected>Selecciona tu país</option>
    <option value="Afghanistan">Afghanistan</option>
    <option value="Albania">Albania</option>
    <option value="Andorra">Andorra</option>
    <option value="Argentina">Argentina</option>
    <option value="Armenia">Armenia</option>
    <option value="Australia">Australia</option>
    <option value="Austria">Austria</option>
    <option value="Azerbaijan">Azerbaijan</option>
    <option value="Bahamas">Bahamas</option>
    <option value="Bahrain">Bahrain</option>
    <option value="Bangladesh">Bangladesh</option>
    <option value="Belarus">Belarus</option>
    <option value="Belgium">Belgium</option>
    <option value="Bhutan">Bhutan</option>
    <option value="Bolivia">Bolivia</option>
    <option value="Bosnia">Bosnia</option>
    <option value="Brazil">Brazil</option>
    <option value="Bulgaria">Bulgaria</option>
    <option value="Canada">Canada</option>
    <option value="Chile">Chile</option>
    <option value="China">China</option>
    <option value="Colombia">Colombia</option>
    <option value="Costa Rica">Costa Rica</option>
    <option value="Croatia">Croatia</option>
    <option value="Cyprus">Cyprus</option>
    <option value="Czech Republic">Czech Republic</option>
    <option value="Denmark">Denmark</option>
    <option value="Ecuador">Ecuador</option>
    <option value="Egypt">Egypt</option>
    <option value="Estonia">Estonia</option>
    <option value="Finland">Finland</option>
    <option value="France">France</option>
    <option value="Georgia">Georgia</option>
    <option value="Germany">Germany</option>
    <option value="Ghana">Ghana</option>
    <option value="Greece">Greece</option>
    <option value="Hong Kong">Hong Kong</option>
    <option value="Hungary">Hungary</option>
    <option value="Iceland">Iceland</option>
    <option value="India">India</option>
    <option value="Indonesia">Indonesia</option>
    <option value="Iraq">Iraq</option>
    <option value="Ireland">Ireland</option>
    <option value="Israel">Israel</option>
    <option value="Italy">Italy</option>
    <option value="Jamaica">Jamaica</option>
    <option value="Japan">Japan</option>
    <option value="Jordan">Jordan</option>
    <option value="Kazakhstan">Kazakhstan</option>
    <option value="Kenya">Kenya</option>
    <option value="Kosovo">Kosovo</option>
    <option value="Kuwait">Kuwait</option>
    <option value="Kyrgyzstan">Kyrgyzstan</option>
    <option value="Latvia">Latvia</option>
    <option value="Lebanon">Lebanon</option>
    <option value="Liechtenstein">Liechtenstein</option>
    <option value="Lithuania">Lithuania</option>
    <option value="Luxembourg">Luxembourg</option>
    <option value="Malaysia">Malaysia</option>
    <option value="Maldives">Maldives</option>
    <option value="Malta">Malta</option>
    <option value="Mexico">Mexico</option>
    <option value="Moldova">Moldova</option>
    <option value="Monaco">Monaco</option>
    <option value="Montenegro">Montenegro</option>
    <option value="Morocco">Morocco</option>
    <option value="Nepal">Nepal</option>
    <option value="Netherlands">Netherlands</option>
    <option value="New Zealand">New Zealand</option>
    <option value="Nigeria">Nigeria</option>
    <option value="North Macedonia">North Macedonia</option>
    <option value="Norway">Norway</option>
    <option value="Oman">Oman</option>
    <option value="Pakistan">Pakistan</option>
    <option value="Panama">Panama</option>
    <option value="Paraguay">Paraguay</option>
    <option value="Peru">Peru</option>
    <option value="Philippines">Philippines</option>
    <option value="Poland">Poland</option>
    <option value="Portugal">Portugal</option>
    <option value="Qatar">Qatar</option>
    <option value="Romania">Romania</option>
    <option value="Russia">Russia</option>
    <option value="San Marino">San Marino</option>
    <option value="Serbia">Serbia</option>
    <option value="Singapore">Singapore</option>
    <option value="Slovakia">Slovakia</option>
    <option value="Slovenia">Slovenia</option>
    <option value="South Africa">South Africa</option>
    <option value="South Korea">South Korea</option>
    <option value="Spain">Spain</option>
    <option value="Sri Lanka">Sri Lanka</option>
    <option value="Sweden">Sweden</option>
    <option value="Switzerland">Switzerland</option>
    <option value="Syria">Syria</option>
    <option value="Taiwan">Taiwan</option>
    <option value="Tajikistan">Tajikistan</option>
    <option value="Thailand">Thailand</option>
    <option value="Trinidad">Trinidad</option>
    <option value="Turkey">Turkey</option>
    <option value="UAE">UAE</option>
    <option value="UK">UK</option>
    <option value="USA">USA</option>
    <option value="Ukraine">Ukraine</option>
    <option value="Uruguay">Uruguay</option>
    <option value="Uzbekistan">Uzbekistan</option>
    <option value="Vatican City">Vatican City</option>
    <option value="Venezuela">Venezuela</option>
    <option value="Vietnam">Vietnam</option>
    <option value="Yemen">Yemen</option>
  </select>
</div>

        </div>

        <!-- Hábitos digitales -->
        <div class="space-y-4">
          <h2 class="text-lg font-medium text-gray-700">Hábitos Digitales</h2>

          <!-- Plataforma más usada -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Plataforma más usada</label>
            <select v-model="formData.platform" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md border">
              <option value="" disabled selected>Selecciona la plataforma que más usas</option>
              <option value="Instagram">Instagram</option>
              <option value="Facebook">Facebook</option>
              <option value="TikTok">TikTok</option>
              <option value="Twitter">Twitter</option>
              <option value="YouTube">YouTube</option>
            </select>
          </div>

          <!-- Horas de uso diario -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">
              Horas de uso diario: {{ formData.dailyUsageHours }} horas
            </label>
            <input
              v-model="formData.dailyUsageHours"
              type="range"
              min="0"
              max="10"
              step="0.5"
              class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer"
            >
            <div class="flex justify-between text-xs text-gray-500">
              <span>0h</span>
              <span>5h</span>
              <span>10h</span>
            </div>
          </div>
        </div>

        <!-- Vida personal -->
        <div class="space-y-4">
          <h2 class="text-lg font-medium text-gray-700">Vida Personal</h2>

          <!-- Estado de relación -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Estado de relación</label>
            <select v-model="formData.relationshipStatus" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md border">
              <option value="" disabled selected>Selecciona tu estado de relación</option>
              <option value="Soltero/a">Soltero/a</option>
              <option value="En una relación">En una relación</option>
              <option value="Complicado">Complicado</option>
            </select>
          </div>

          <!-- Horas de sueño -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">
              Horas de sueño promedio: {{ formData.sleepHours }} horas
            </label>
            <input
              v-model="formData.sleepHours"
              type="range"
              min="0"
              max="10"
              step="0.5"
              class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer"
            >
            <div class="flex justify-between text-xs text-gray-500">
              <span>0h</span>
              <span>6h</span>
              <span>10h</span>
            </div>
          </div>
        </div>

        <!-- Botón de envío -->
        <div>
          <button
            type="submit"
            class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          >
            Enviar Encuesta
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const formData = ref({
  gender: '',
  academicLevel: '',
  country: '',
  platform: '',
  dailyUsageHours: 2,
  relationshipStatus: '',
  sleepHours: 7,
  // Los siguientes campos se calcularán automáticamente
  academicImpact: 0,
  mentalHealth: 0,
  conflicts: 0,
  addictionLevel: 0
})

const submitForm = () => {
  // Aquí puedes agregar la lógica para calcular los campos no seleccionables
  // basado en las respuestas del usuario

  // Ejemplo de cálculo simple (deberías ajustar esto según tu lógica real)
  formData.value.academicImpact = calculateAcademicImpact()
  formData.value.mentalHealth = calculateMentalHealth()
  formData.value.conflicts = calculateConflicts()
  formData.value.addictionLevel = calculateAddictionLevel()

  console.log('Datos enviados:', formData.value)
  // Aquí iría la lógica para enviar los datos al servidor
}

// Funciones de ejemplo para calcular los campos no seleccionables
const calculateAcademicImpact = () => {
  // Lógica para calcular cómo afecta académicamente
  return Math.random() * 10 // Ejemplo - reemplazar con lógica real
}

const calculateMentalHealth = () => {
  // Lógica para calcular salud mental
  return Math.random() * 10 // Ejemplo - reemplazar con lógica real
}

const calculateConflicts = () => {
  // Lógica para calcular conflictos
  return Math.random() * 10 // Ejemplo - reemplazar con lógica real
}

const calculateAddictionLevel = () => {
  // Lógica para calcular nivel de adicción
  return Math.random() * 10 // Ejemplo - reemplazar con lógica real
}
</script>

<style scoped>


input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #4f46e5;
  cursor: pointer;
}
</style>
