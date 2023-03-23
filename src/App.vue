<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
