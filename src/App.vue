<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você tem <strong> {{ getPendentes().length }} </strong> tarefas pendentes.</p>
    </header>

    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input type="text" class="form-control" placeholder="Digite uma tarefa" required @change="e => estado.tarefaTemp = e.target.value" :value="estado.tarefaTemp"/>
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Adicionar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="(e) => estado.filtro = e.target.value">
            <option value="todas">Todas</option>
            <option value="pendente">Pendentes</option>
            <option value="concluida">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getFiltradas()">
        <input type="checkbox" :checked="tarefa.concluida" :id="tarefa.titulo" @change="e => tarefa.concluida = e.target.checked"/>
        <label :class="{ done: tarefa.concluida }" class="ms-3" :for="tarefa.titulo"> {{ tarefa.titulo }} </label>
      </li>
    </ul>
  </div>

</template>

<style scoped>

.done {
  text-decoration: line-through;
}

</style>
