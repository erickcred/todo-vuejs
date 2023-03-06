<script setup>
import { reactive } from 'vue';

import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaTarefas from './components/ListaTarefas.vue';


const estado = reactive({
  filtro: "todas",
  tarefaTemporaria: "",
  tarefas: [
    {
      titulo: "Estudar ES6",
      finalizada: false
    },
    {
      titulo: "Estudar SASS",
      finalizada: false
    },
    {
      titulo: "Estudar HTML",
      finalizada: true
    }
  ]
});


const getTarefasPendentes = () => {
  return estado.tarefas.filter( tarefa => !tarefa.finalizada );
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter( tarefa => tarefa.finalizada );
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }

}

const cadastrarNovaTarefa = () => {
  const terefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false
  };
  estado.tarefas.push(terefaNova);
  estado.tarefaTemporaria = "";
}

</script>



<template>
  
  <div class="container">
    <Cabecalho 
      :get-tarefas-pendentes="getTarefasPendentes().length" 
    />

    <Formulario 
      :cadastrar-nova-tarefa="cadastrarNovaTarefa"
      :tarefa-temporaria="estado.tarefaTemporaria"
      :trocarFiltro="evento => estado.filtro = evento.target.value"
      :edita-trarefa-temporaria="evento => estado.tarefaTemporaria = evento.target.value"
    />
    
    <ListaTarefas 
      :get-tarefas-filtradas="getTarefasFiltradas()"
      :tem-tarefas-pendentes="getTarefasFiltradas().length"
      :tipo-filtro="estado.filtro"
    />
  </div>

</template>



<style scoped>

</style>
