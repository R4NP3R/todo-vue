<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas', 
    tarefaTemp: '',   
    tarefas: [
      {
      titulo: 'Estudar CSS',
      finalizada: false,
      },
      {
      titulo: 'Estudar JavaScript',
      finalizada: false,
      },
      {
      titulo: 'Ir para academia',
      finalizada: true,
      }
    ]
  }) 

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefas => !tarefas.finalizada);
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefas => tarefas.finalizada);
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'concluidas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
}

  const cadastraTarefa = () => {
      const tarefaNova = {
        titulo: estado.tarefaTemp,
        estado: false
      }
      estado.tarefas.push(tarefaNova);
      estado.tarefaTemp = '';
  }
  
</script>

<template>
  <div class="container">
    <header class="p-5 mb-5 mt-5 bg-light rounded-3">
      <h1>
        Minhas Tarefas
      </h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
        <input :value="estado.tarefaTemp" required @change="evento => estado.tarefaTemp = evento.target.value" type="text" placeholder="Digite a descrição da Tarefa" class="form-control">
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas Tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="concluidas">Concluidas</option>
        </select>
      </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" :for="tarefa.titulo" class="ms-3">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
