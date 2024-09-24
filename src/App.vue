
<script setup>
import { ref, reactive } from 'vue';
import { uid } from 'uid';
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Paciente from './components/Paciente.vue';

const pacientes = ref([]);

const paciente = reactive({
    id: null,
    nombre: '',
    propitario: '',
    email: '',
    alta:'',
    sintomas:''

});

const agregarPaciente = ()=>{

  if(paciente.id){
    const {id} = paciente
    const i = paciente.value.findIndex((pacienteState)=> pacienteState.id === id)
    paciente.value[i] = {...paciente}
     
  }else {
    pacientes.value.push({...paciente, id: uid()})
    
  }

 

  // reiniciar el objeto
  paciente.nombre = ''
  paciente.propitario = ''
  paciente.email = ''
  paciente.alta = ''
  paciente.sintomas = ''
  paciente.id = ''

}


const actualizarPaciente = (id) => {
  const pacienteEditar = pacientes.value.filter( paciente => paciente.id === id)[0]
  
    Object.assign(paciente, pacienteEditar)
  
}

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex">
      
      <Formulario

        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propitario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @agregar-paciente="agregarPaciente"
      
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">

        <h3 class="font-black text-3xl text-center">
          Administra tus Pacientes
        </h3>

        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
           Informacion de
            <span class="text-indigo-500 font-bold">Pacientes</span>
        </p>

          <Paciente
          v-for="paciente in pacientes"
          :paciente="paciente"
          :key="paciente.id"
          @actualizar-paciente="actualizarPaciente"
       
          
          />

        </div>

        <p v-else class="mt-20 text-2xl text-center">
          No hay pacientes

        </p>

      </div>
      
    </div>

  </div>


  
</template>

<style lang="scss" scoped>

</style>