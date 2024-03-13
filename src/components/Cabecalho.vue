<script setup>
const propriedades = defineProps(['tarefasPendentes']);
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p>
            Voce possui {{ propriedades.tarefasPendentes}} tarefas pendentes
        </p>
    </header>
</template>