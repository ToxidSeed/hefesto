<template>
    <q-dialog v-model="localValue">
        <q-card>
            <q-toolbar>
                <q-avatar icon="question_mark" color="orange-10" class="text-white"/>
                <q-toolbar-title class="text-subtitle1 text-orange-10">
                    {{ config.title }}
                </q-toolbar-title>
            </q-toolbar>
            <q-separator/>
            <q-card-section class="row items-center">
            <!--<q-avatar icon="question_mark" text-color="blue-10"/>-->
            <span class="q-ml-sm text-subtitle2">{{config.msg}}</span>
            </q-card-section>

            <q-card-actions align="right">
                <q-btn label="Si" color="primary" v-close-popup @click="btn_si_click_handler"/>
                <q-btn flat label="Cancel" color="red" v-close-popup />            
            </q-card-actions>
        </q-card>
    </q-dialog>
</template>
<script>
export default {
    name:"Confirmar",
    props:{
        value:{
            required:true
        },
        msg:{
            type:String,
            default:""
        },
        config:{
            type: Object,
            default: () => {
                return {
                    title:"",
                    msg:"",
                    callback:"ok"
                }
            }
        }
    },
    data(){
        return {
            localValue:this.value
        }
    },
    watch:{
        localValue:function(newval){
            this.$emit('input', newval)
        },
        value:function(newval){
            this.localValue = newval
        }
    },
    methods:{
        btn_si_click_handler:function(){
            this.localValue = false
            this.$emit(this.config.callback)
        }
    }
}
</script>