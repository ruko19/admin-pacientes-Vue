<script setup>
import { ref, reactive, computed } from 'vue';
import Alerta from './Alerta.vue';

const alerta = reactive({
    tipo:'',
    mensaje:''
})

 const emit = defineEmits(['update:nombre', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'agregar-paciente'])

const props = defineProps({
    id:{
        type: [String,null],
        require:true

    },
    nombre: {
        type: String,
        require: true
    },
    propietario: {
        type: String,
        require: true
    },
    email: {
        type: String,
        require: true
    },
    alta: {
        type: String,
        require: true
    },
    sintomas: {
        type: String,
        require: true
    },

})



const validar = ()=>{
   if(Object.values(props).includes('')){
    alerta.mensaje = 'Todos los campos son obligatorios.'
    alerta.tipo = 'error'
    return
    
   }

   emit('agregar-paciente') 
   alerta.mensaje = 'Paciente agregado Correctamente'
   alerta.tipo = 'exito'


   setTimeout(()=>{
    Object.assign(alerta,{
        tipo:'',
         mensaje:''

    })

   },3000)
}


const editando = computed(() =>{
    return props.id
})

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="text-3xl font-black text-center">Seguimiento Pacientes</h2>

        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-500 font-bold">Administralos</span>
        </p>

        <Alerta 
            v-if="alerta.mensaje"
            :alerta="alerta"
        />

        <form @submit.prevent="validar" class="bg-white shadow-md rounded-lg py-10 px-5 mb-10">

            <div class="mb-5">
                
                <label for="mascota" class="block text-gray-700 uppercase font-bold">
                    Nombre Mascota
                </label>
                <input 
                    id="mascota" 
                    type="text" 
                    placeholder="Nombre de la mascota" 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="nombre"
                    @input="$emit('update:nombre',$event.target.value)"
                />

            </div>

            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">
                    Nombre del Propietario
                </label>
                <input 
                    id="propietario" 
                    type="text" 
                    placeholder="Nombre del propietario" 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="propietario"
                    @input="$emit('update:propietario',$event.target.value)"
                />

            </div>
            <div class="mb-5">
                <label for="Email" class="block text-gray-700 uppercase font-bold">
                    Email
                </label>
                <input 
                    id="Email" 
                    type="text" 
                    placeholder="Email del propietario" 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="email"
                    @input="$emit('update:email',$event.target.value)"
                />

            </div>
            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">
                    Alta
                </label>
                <input 
                    id="alta" 
                    type="date" 
                    placeholder="Email del propietario" 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="alta"
                    @input="$emit('update:alta',$event.target.value)"
                />

            </div>
            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">
                    Sintomas
                </label>
                <textarea 
                    id="sintomas" 
                    
                    placeholder="Describe los sintomas." 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40"
                    :value="sintomas"
                    @input="$emit('update:sintomas',$event.target.value)"
                />

            </div>

            <input 
              type="submit"
              class="bg-indigo-500 w-full p-3 text-white uppercase font-bold cursor-pointer hover:bg-indigo-700 transition-colors"
              :value="[editando ? 'Guardar Cambios' : 'Registrar Paciente']"
            />
            

        </form>

    </div>
</template>
