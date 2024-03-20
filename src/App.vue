
<template>

  <!-- Calendário-->
  <h3>Calendário:</h3>
  <VueDataPicker v-model="dataSelecionada"
    inline auto-apply
    :format-locale="ptBR"
    format="P"
    :locale="localeConfig"></VueDataPicker>
  <div id="app">

    <h2>Lista de Tarefas da Claudia</h2>

    <input 
      placeholder=" Adicione uma tarefa" 
      type="text" 
      v-model="novaTarefa" 
      v-on:keyup.enter="adicionarTarefa" 
      :disabled = "edicaoAtiva">
    <button v-on:click="adicionarTarefa"> Adicionar</button>
    <ul>
      <li v-for="(tarefa, index) in tarefas" :key="index">
        <span v-if="!tarefaEditando[index]"> {{ tarefa }}</span>
        <input v-else type="text" v-model="tarefas[index]" v-on:blur="concluirEdicao(index)" v-on:keyup.enter="concluirEdicao(index)">
        <div>
          <button v-on:click="editarTarefa(index)" > {{ tarefaEditando[index] ? 'Concluir' : 'Editar'}}</button>
          <button v-on:click="removerTarefa(index)" >Remover</button>
        </div>
      </li>
    </ul>
    </div>
</template>



<!--COMPOSITION API  inicio -->
<script setup>
import { computed, ref } from 'vue'
import { ptBR } from 'date-fns/locale';
import VueDataPicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'


//variavel reativa para armazenar as novas tarefas
const novaTarefa = ref('');

//array reativo para armazenar as tarefas
const tarefas = ref([]);

//array reativo para armazenar o estado de edição das tarefas
const tarefaEditando = ref([]);

const edicaoAtiva = computed(() => tarefaEditando.value.some(estado => estado));

const adicionarTarefa = () => {
  if (novaTarefa.value.trim() !== '') {
    tarefas.value.push(novaTarefa.value);
    //a tarefa nao está sendo editada
    tarefaEditando.value.push(false);
    novaTarefa.value = '';
  }
};

//variavel reativa para data do calendario
const dataSelecionada = ref( new Date());

const removerTarefa = (index) => {
  tarefas.value.splice(index, 1);
  //remove o estado de edição 
  tarefaEditando.value.splice(index,1) 
};


//função para iniciar a edição de uma tarefa
const editarTarefa = (index) => {
  if (!tarefaEditando.value[index]){
    tarefaEditando.value[index] = true;
  }
};

const concluirEdicao = (index) => {
  tarefaEditando.value[index] = false;
}

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
  width: 500px;
}

input[type="text"] {
  width: 70%;
  padding: 10px;
  margin-bottom: 10px;
}

ul {
  list-style-type: none;
  padding: 10px;
  margin-bottom: 10px;
}

li {
  margin-bottom: 10px;
  margin-left: 10px;
}

button {
  padding: 5px 10px;
  background-color: #50c0ba;
  color: #fff;
  border: none;
  margin: 10px;
}
</style>