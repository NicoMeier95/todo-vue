<template>
    <h1 class="text-center text-white my-5">T O D O</h1>
    <todo-form />
    <todo-list />
</template>

<script>
import { ref , provide, watchEffect} from 'vue';
import TodoForm from './TodoForm.vue';
import TodoList from './TodoList.vue';


export default {
    components:{TodoForm, TodoList},
    setup() {
        const todos = ref([]);
        provide('todos', todos);

        if(localStorage.getItem('todos')){
            todos.value = JSON.parse(localStorage.getItem('todos'))
        }

        watchEffect(()=>{
            localStorage.setItem('todos',JSON.stringify(todos.value))
        })
    }
}
</script>

<style>
body{
    background-image: url('../assets/bg-desktop-light.jpg');
    background-repeat: no-repeat;
    background: linear-gradient hsl(192, 100%, 67%) to hsl(280, 87%, 65%);
}

@media (max-width: 468px) {
    h1{
        display: flex;
        margin-left: 5%;
    }
}
</style>