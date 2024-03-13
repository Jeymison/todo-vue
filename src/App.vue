<script setup>
import { reactive } from 'vue';
// Importando os componentes
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  tarefaTemporaria: '',

  filtro: 'todas',

  tarefas: []
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada) // falsa
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada) // verdadeiro
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
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
    <!-- Chamando os Componentes -->
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefaTemporaria="estado.tarefaTemporaria" :edita-tarefa-temp="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>
