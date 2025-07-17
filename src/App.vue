<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import Tarefas from './components/Tarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6+',
      concluida: false
    },
    {
      titulo: 'Estudar Vue.js',
      concluida: false
    },
    {
      titulo: 'Estudar Bootstrap',
      concluida: true
    },
  ]
})

const getPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.concluida);
}

const getFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.concluida);
}

const getFiltradas = () => {
  const filtro = estado.filtro;

  switch (filtro) {
    case 'pendente':
      return getPendentes();
    case 'concluida':
      return getFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastrarTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    concluida: false
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = '';
}

</script>

<template>

  <div class="container">
    <Cabecalho :tarefas-pendentes="getPendentes().length"/>
    <Formulario :tarefa-temp="estado.tarefaTemp" :editar-tarefa="e => estado.tarefaTemp = e.target.value" :cadastrar-tarefa="cadastrarTarefa" :trocar-filtro="e => estado.filtro = e.target.value"/>
    <Tarefas :tarefas="getFiltradas()"/>
  </div>

</template>