<template>
    <div class="card">
       <div class="card-body d-flex justify-content-between align-items-center">
           <span 
            role="button"
            @click="filtrar('active')"
            >
               Actives
           </span>
           <span 
            role="button"
            @click="filtrar('all')"
           >
               All
           </span>
           <span 
            role="button"
            @click="filtrar('completed')"
           >
               Completed
           </span>
       </div>
    </div>
</template>

<script>
import { inject } from '@vue/runtime-core'
    export default {
        setup() {
            const estado = inject('estado');

            const filtrar = valor =>{
                estado.value = valor
            }

            return {filtrar}
        }
    }
</script>

<style>

</style>