<template>
  <form @submit.prevent="agregarTarea">
        <input 
            type="text"
            class="form-control my-3 p-2 text-center"
            placeholder="Ingrese tarea"
            v-model.trim="texto"
        >
  </form>
</template>

<script>
import { ref, inject  } from 'vue'
export default {
    setup() {
      const todos = inject('todos');
      const texto = ref('');
      const agregarTarea = ()=>{
        if(texto.value === ''){
          console.log('Debes escribir algo');
          return
        }
        
        const todo = {
        texto : texto.value,
        estado: false,
        id: Date.now(),
        }

        todos.value.push(todo);

        texto.value= '';
      };
      
      
      
      return{
        agregarTarea, texto, todos
      }
    }
}
</script>

<style>
form{
  width: 50%;
  min-width: 450px;
  display: flex;
  justify-content: center;
  margin: 0 auto
}

@media (max-width: 468px) {
  form{
    width: 95%;
    min-width: 100px;
    max-width: 450px;
  }
}
</style>