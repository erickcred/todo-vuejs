<script setup>
    const props = defineProps(['getTarefasFiltradas', 'finalizaTarefa', 'temTarefasPendentes', 'tipoFiltro'])
</script>

<template>
  <ul class="list-group mt-4" v-if="(!(props.temTarefasPendentes < 1 && tipoFiltro == 'pendentes'))">
    <li class="list-group-item" v-for="tarefa in props.getTarefasFiltradas">
      <input
        @change="(evento) => (tarefa.finalizada = evento.target.checked)"
        type="checkbox"
        :checked="tarefa.finalizada"
        :id="tarefa.titulo"
      />
      <label
        :class="{ done: tarefa.finalizada }"
        class="ms-3"
        :for="tarefa.titulo"
        >{{ tarefa.titulo }}</label
      >
    </li>
  </ul>
  <h3 v-else class="text-center mt-4">Não há tarefas pendentes no momento</h3>


</template> 

<style scoped>
.done {
  text-decoration: line-through;
}
</style>