<template>
  <div id="app">
    <h2>Lista de Tarefas da Claudia</h2>
    <input placeholder=" Adicione uma tarefa" type="text" v-model="novaTarefa" v-on:keyup.enter="addTarefa">
    <button v-on:click="addTarefa"> Adicionar</button>
    <ul>
      <li v-for="(todo, index) in tarefas" :key="index">   
        {{ todo }}     
      <button v-on:click="removeTarefa(index)" >Remover</button>
      </li>
    </ul>
    </div>
</template>

<!--COMPOSITION API  inicio -->
<script setup>
import { ref } from 'vue'

const novaTarefa = ref('');
const tarefas = ref([]);

const addTarefa = () => {
  if (novaTarefa.value.trim() !== '') {
    tarefas.value.push(novaTarefa.value);
    novaTarefa.value = '';
  }
};

const removeTarefa = (index) => {
  tarefas.value.splice(index, 1);
};


</script>   
<!-- fim  -->





<!--   OPTIONS API   inicio
<script>
export default {
  data(){
    return {
      novaTarefa: '',
      tarefas:[]
    }
  },
  methods:{
    addTarefa(){
      if( this.novaTarefa.trim() !== ''){
        this.tarefas.push(this.novaTarefa);
        this.novaTarefa = '';
      }
    },
    removeTarefa(index){
      this.tarefas.splice(index,1);
    }
  }
}
</script>
fim -->


<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app {
  width: 300px;
}

input[type="text"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
}

ul {
  list-style-type: none;
  padding: 10px;
}

li {
  margin-bottom: 50px;
}

button {
  padding: 5px 10px;
  background-color: #50c0ba;
  color: #fff;
  border: none;
  margin-bottom: 30px;
}
</style>