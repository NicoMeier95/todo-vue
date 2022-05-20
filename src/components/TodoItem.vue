<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
        <span 
            role="button" 
            @click="completarTarea(todo.id)"
            :class="{'tachado' : todo.estado}"    
        >
            {{todo.texto}}
        </span>
        <span role="button" @click="eliminarTarea(todo.id)">
            <i class="fa-solid fa-x"></i>
        </span>
    </li>
</template>

<script>
import { inject } from '@vue/runtime-core'
export default {
    props:{
        todo:{
            type: Object,
            required: true
        }
    },
    setup(){
        const todos = inject('todos')
        const eliminarTarea = id => {
            todos.value = todos.value.filter(item => item.id !== id)
        }
        const completarTarea = id =>{
            todos.value = todos.value.map(item => {
                if(item.id === id){
                    item.estado = true
                }
                return item
            })
        }
        return {eliminarTarea, completarTarea}
    }
}
</script>

<style>
.tachado {
    text-decoration: line-through;
}
</style>