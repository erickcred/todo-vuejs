<script setup>
import { reactive } from 'vue';


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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possiu {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>

    <form action="" @submit.prevent="cadastrarNovaTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" required>
        </div>

        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>

        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
        <label :class="{ done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
    

  </div>

</template>



<style scoped>
.done {
  text-decoration: line-through;
}
</style>
