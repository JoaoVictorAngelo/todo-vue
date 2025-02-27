<script setup>
  import { reactive  } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefa: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Ir para academia',
        finalizada: true,
      }
    ]
  })

  const getTarefasaPendentes = () => {
    return estado.tarefa.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasaFinalizadas = () => {
    return estado.tarefa.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasaPendentes();
      case 'finalizadas':
        return getTarefasaFinalizadas();
      default:
        return estado.tarefa;
    }
  }

  const cadastrarTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefa.push(tarefaNova)
    estado.tarefaTemp = ''
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasaPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastrar-tarefa="cadastrarTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>