<script setup>
const { cadastrarTarefa, tarefaTemp, trocarFiltro, editarTarefa } = defineProps([
    'cadastrarTarefa',
    'tarefaTemp',
    'trocarFiltro',
    'editarTarefa'
])
</script>

<template>
    <form @submit.prevent="cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input type="text" class="form-control" placeholder="Digite uma tarefa" required @change="editarTarefa"
                    :value="tarefaTemp" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Adicionar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="trocarFiltro">
                    <option value="todas">Todas</option>
                    <option value="pendente">Pendentes</option>
                    <option value="concluida">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>