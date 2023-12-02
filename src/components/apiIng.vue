
  
<script setup>
import { ref, onMounted } from 'vue';

const info = ref(null);

const fetchData = async () => {
  try {
    const response = await fetch('https://sitmotul.com.mx/api/statusEvalIng');
    info.value = await response.json();

    console.log("Datos de las carreras:", info.value);
  } catch (error) {
    console.log('Error al obtener datos: ', error);
  }
};

onMounted(() => {
  fetchData();
});
</script>

<template>
  
 <div class="ml-4 mr-4 bg-indigo-300">
  <div class="flex items-center justify-center">
  <p class="text-3xl font-bold ms-8">Estado de la evaluación por ingeniería</p>
</div>
  <div class="grid grid-cols-2 sm:grid-cols-5 gap-2 place-content-center p-4 sm:p-8 ml-4 ">
    <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 ">
      <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 flex flex-col items-center justify-center text-center">
        <div v-if="info">
          
          <p class="text-4xl font-bold">{{ info.ISC.listas !== 0 ? (100 / 244 * info.ISC.listas).toFixed(1) + "%" : 'N/A' }} </p>
          <p class="text-1 font-bold">Sistemas Computacionales</p>
        </div>
              <p v-if="info && info.ISC">ISC - Listas: {{ info.ISC.listas }}, Faltantes: {{ info.ISC.faltantes }}</p>
      </div>
  </div>

    <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 transition ease-in-out delay-150 bg-blue-500 hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500 duration-300 ">
      <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 flex flex-col items-center justify-center text-center">
        <div v-if="info">
          
          <p class="text-4xl font-bold">{{ info.IEM.listas !== 0 ? (100 / (info.IEM.listas + info.IEM.faltantes)* info.IEM.listas).toFixed(1) + "%" : 'N/A' }} </p>
          <p class="text-1 font-bold">Electromecánica</p>
        </div>
      <p v-if="info && info.IEM">IEM - Listas: {{ info.IEM.listas }}, Faltantes: {{ info.IEM.faltantes }}</p>
    </div>
  </div>

  <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 transition ease-in-out delay-150 bg-blue-500 hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500 duration-300 ">
      <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 flex flex-col items-center justify-center text-center">
        <div v-if="info">
          <p class="text-4xl font-bold">{{ info.IER.listas !== 0 ? ((100 / (info.IER.listas + info.IER.faltantes)) * info.IER.listas).toFixed(1) + "%" : 'N/A' }} </p>
          <p class="text-1 font-bold">Energias Renovables</p>
        </div>
      <p v-if="info && info.IER">IER - Listas: {{ info.IER.listas }}, Faltantes: {{ info.IER.faltantes }}</p>
    </div>
  </div>

  <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 transition ease-in-out delay-150 bg-blue-500 hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500 duration-300 ">
      <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 flex flex-col items-center justify-center text-center">
        <div v-if="info">
          <p class="text-4xl font-bold">{{ info.IE.listas !== 0 ? ((100 / (info.IE.listas + info.IE.faltantes)) * info.IE.listas).toFixed(1) + "%" : 'N/A' }} </p>
        </div>
        <p class="text-1 font-bold">Electrónica</p>
      <p v-if="info && info.IE">IE - Listas: {{ info.IE.listas }}, Faltantes: {{ info.IE.faltantes }}</p>
    </div>
  </div>

  <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 transition ease-in-out delay-150 bg-blue-500 hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500 duration-300 ">
      <div class="rounded-lg bg-indigo-500 h-40 sm:h-60 w-32 sm:w-32 flex flex-col items-center justify-center text-center">
        <div v-if="info">
          <p class="text-4xl font-bold">{{ info.II.listas !== 0 ? ((100 / (info.II.listas + info.II.faltantes)) * info.II.listas).toFixed(1) + "%" : 'N/A' }} </p>
        </div>
        <p class="text-1 font-bold">Industrial</p>
        <p v-if="info && info.II">II - Listas: {{ info.II.listas }}, Faltantes: {{ info.II.faltantes }}</p>
    </div>
  </div>

</div>
</div>







</template>





<script>


</script>


