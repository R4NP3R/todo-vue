<script setup>
const props = defineProps(['cadastraTarefa', 'tarefaTemp','trocarFiltro','editaTarefaTemp' ])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" required @change="props.editaTarefaTemp"
                    type="text" placeholder="Digite a descrição da Tarefa" class="form-control">
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="concluidas">Concluidas</option>
                </select>
            </div>
        </div>
    </form>
</template>