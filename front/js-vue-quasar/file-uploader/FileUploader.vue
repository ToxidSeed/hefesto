<template>
    <div>
        <q-file
            v-model="fichero"
            label="Seleccionar fichero de opciones"
            use-chips        
            stack-label                
        >                
            <template v-slot:prepend>
            <q-icon name="attach_file" />
            </template>
        </q-file>
        <q-input label="nombre" v-model="nombre"/>
        <q-btn label="Aceptar" @click="procesar"/>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    name:"FileUploader",
    data() {
        return {
            nombre:"",
            fichero:null
        }
    },
    methods:{
        procesar:function(){
            let form_data = new FormData();
            form_data.append("nombre",this.nombre)
            form_data.append("fichero", this.fichero)
            let config = {
                headers:{
                    'Content-Type':"multipart/form-data"
                }
            }

            axios.post(
                'resource',
                form_data,
                config
            ).then(httpresp => {
                console.log(httpresp)
            })
        }
    }
}
</script>