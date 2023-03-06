<script setup>
    const props = defineProps(['cadastrarNovaTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTrarefaTemporaria'])
</script>

<template>
    <form action="" @submit.prevent="props.cadastrarNovaTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporaria" @change="props.editaTrarefaTemporaria"
                    type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" required>
            </div>

            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>

            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>
