<script setup>
import { reactive } from 'vue';

const estado = reactive({
  tarefaTemporaria: '',

  filtro:'todas',

  tarefas: [
  {
    titulo: 'Estudar ES6',
    finalizada: false,
  },
  {
    titulo: 'Estudar SASS',
    finalizada: false,
  },
  {
    titulo: 'Ir malhar',
    finalizada: true,
  }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada) // falsa
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada) // verdadeiro
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch(filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
    
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemporaria = '';
}
</script>

<template>
<div class="container">

  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Minhas Tarefas</h1>
    <p>
      Voce possui {{ getTarefasPendentes().length }} tarefas pendentes
    </p>
  </header>

  <!-- // para atualizar o cadastro com o novo item usamos .prevent -->
  <form @submit.prevent="cadastraTarefa"> 
  <div class="row">
    <div class="col">
      <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
    </div>
    <div class="col-md-1">
      <button type="submit" class="btn btn-primary">Cadastrar</button>
    </div>
    <div class="col-md-2">
      <select @change="evento => estado.filtro = evento.target.value" class="form-control">
        <option value="todas">Todas as tarefas</option>
        <option value="pendentes">Pendentes</option>
        <option value="finalizadas">Finalizadas</option>
      </select>
    </div>
  </div>
  </form>

  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
      <label :class="{done: tarefa.finalizada == true}" class="ms-3" :for="tarefa.titulo">
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
