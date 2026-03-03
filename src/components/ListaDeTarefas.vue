<script setup>
defineProps(['tarefas'])
</script>

<template>
  <ul v-if="tarefas.length > 0" class="list-group mt-4">
    <li
      class="list-group-item"
      v-for="tarefa in tarefas"
      :key="tarefa.titulo"
    >
      <input
        type="checkbox"
        :checked="tarefa.finalizado"
        @change="evento => tarefa.finalizado = evento.target.checked"
        :id="tarefa.titulo"
      >

      <label
        class="ms-2"
        :for="tarefa.titulo"
        :class="{ done: tarefa.finalizado }"
      >
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>

  <p v-else class="mensagem-vazia">
    Não possui tarefas para exibir.
  </p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

.mensagem-vazia {
  margin-top: 15px;
  padding: 15px;
  background-color: #f0f0f0;
  border-radius: 5px;
  text-align: center;
  color: #555;
  font-weight: bold;
}
</style>