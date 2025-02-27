<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header class="p-5 mt-4 mb-4 bg-light rounded-5">
        <h1>Minhas Tarefas</h1>
        <p>
            Você Possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>