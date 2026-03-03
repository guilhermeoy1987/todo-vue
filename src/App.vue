<script setup>
import { reactive } from 'vue'
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  filtro: "todas",
  tarefaTemp: '',
  tarefas: [
    { titulo: "Estudar ES6", finalizado: false },
    { titulo: "Estudar SASS", finalizado: false },
    { titulo: "Ir para a academia", finalizado: true }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(t => !t.finalizado)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(t => t.finalizado)
}

const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes':
      return getTarefasPendentes()
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}

const cadastraTarefa = () => {
  if (!estado.tarefaTemp.trim()) return

  estado.tarefas.push({
    titulo: estado.tarefaTemp,
    finalizado: false
  })

  estado.tarefaTemp = ''
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />

    <Formulario
      v-model="estado.tarefaTemp"
      :cadastra-tarefa="cadastraTarefa"
      :trocar-filtro="evento => estado.filtro = evento.target.value"
    />

    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>