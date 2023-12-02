
  
  <script setup>
  import { ref, onMounted, computed } from 'vue';
  import dayjs from 'dayjs';

  const info = ref({
    periodo: "",
    alTotal: "",
    alEvaluados: "",
    inicio: "",
    fin: "",
  });



  

  const formatoFechaInicio = computed(() => {
  // Asume que info.inicio contiene la fecha en formato ISO
  return dayjs(info.value.inicio).format('DD-MM-YYYY');
});

const formatoFechaFin = computed(()=>{
    return dayjs(info.value.fin).format('DD-MM-YYYY')
})

const diferenciaHoras = computed(()=>{
  const now = dayjs();
  const finDia = dayjs(info.value.fin);
  
  // Obtener la diferencia en horas
  const diferenciaHora = finDia.diff(now, 'hour');

  return diferenciaHora;
})
  
  const fetchData = async () => {
    try {
      const response = await fetch('https://sitmotul.com.mx/api/statusEval');
      const data = await response.json();
      info.value = data;
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
  <div class="place-content-center bg-blue-400  bg-blend-multiply p-8">
   <div class="flex items-center justify-center">
  <div class="flex flex-col">
    <div>
      <img src="Recursos/logo.svg" class="w-32 h-32 ml-6" alt="logo">
      <p class="text-4xl font-bold">SIT Motul</p>
    </div>
    <div  >
      <p class="text-1xl  mb-2" v-if="info && info.periodo"> Estado de la evaluación <br> del tutor del Periodo: {{  info.periodo }}</p>
    </div>
  </div>
</div>
<div class="grid grid-cols-1 md:grid-cols-2 gap-2 place-content-between mx-auto my-auto md:ml-1/2 md:w-4/5 lg:w-3/5 xl:w-2/5">  
      <p class="text-1xl font-bold rounded-tl rounded-br md:rounded-none w-full md:w-28 md:ml-20 md:rounded-br md:rounded-lg ms-8" v-if="info && info.alTotal">Total de alumnos: {{ info.alTotal + " alumnos" }}</p>
      <p class="text-1xl font-bold w-full md:w-28 rounded-br md:rounded-lg md:ml-0 ml-0 md:mt-0 mt-2  ms-8" v-if="info && info.alEvaluados">Alumnos evaluados: {{ info.alEvaluados + " alumnos" }}</p>
    </div>
<div class="flex items-center justify-center mt-2">
<div class="flex flex-col-reverse">
  <div class="p-2  bg-rose-300 rounded-br rounded-lg p-2"><p  class="text-xl " v-if="info && info.fin">Fin: {{ formatoFechaFin }}</p></div>
  <div class="p-2  bg-green-400 rounded-br rounded-lg "><p  class="text-xl " v-if="info && info.inicio">Inicio: {{ formatoFechaInicio }}</p></div>
 
</div>
</div>

<div class="flex items-center justify-center py-8">
<div class="flex flex-col-reverse  bg-amber-200 p-2 rounded-tl rounded-br rounded-lg">
    <p  class="text-xl " v-if="info && info.fin">Tiempo por concluir {{ diferenciaHoras + "h"}}</p>
  </div>
</div>
</div>
</div>

  </template>