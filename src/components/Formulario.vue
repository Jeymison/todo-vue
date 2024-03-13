<script setup>
const propriedades = defineProps(['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="propriedades.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="propriedades.tarefaTemporaria" @change="propriedades.editaTarefaTemp" required type="text"
                    placeholder="Digite aqui a descrição da tarefa" class="form-control" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="propriedades.trocarFiltro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>