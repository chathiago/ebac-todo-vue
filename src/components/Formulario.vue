<script setup>
    const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro', 'editarTarefa']);
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input type="text" class="form-control" placeholder="Digite uma tarefa" required
                    @change="props.editarTarefa" :value="props.tarefaTemp" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Adicionar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.trocarFiltro">
                    <option value="todas">Todas</option>
                    <option value="pendente">Pendentes</option>
                    <option value="concluida">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>