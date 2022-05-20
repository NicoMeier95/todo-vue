<template>
    <ul class="list-group mt-5">
        <todo-item 
            v-for="todo in todos" :key="todo.id"
            :todo="todo"
        />
        <li v-if="todos.length === 0" class="list-group-item">
            No hay ToDos...
        </li>
        <todo-footer 
            v-if="todos.length !== 0"
        />

        <todo-filter />
    </ul>
</template>

<script>
import { computed, inject, provide, ref } from 'vue'
import TodoItem from './TodoItem.vue'
import TodoFooter from './TodoFooter.vue'
import TodoFilter from './TodoFilter.vue'
export default {
    components:{TodoItem, TodoFooter, TodoFilter},
    setup() {
        const todosAll = inject('todos');
        const estado = ref('all');
        
        const todos = computed(() => {
            if(estado.value==='all'){
                return todosAll.value
            }
            if(estado.value==='active'){
                return todosAll.value.filter(item => item.estado===false)
            } 
            if(estado.value==='completed'){
                return todosAll.value.filter(item => item.estado===true)
            }
        });
        
        provide('estado',estado)

        return{
            todos
        }
    }
}
</script>

<style>
ul{
    width: 50%;
    min-width: 468px;
    display: flex;
    justify-content: center;
    margin: 0 auto
}

@media (max-width: 468px) {
  ul{
    width: 95%;
    min-width: 100px;
    max-width: 450px;
    margin-top: 10px !important;
  }
}
</style>