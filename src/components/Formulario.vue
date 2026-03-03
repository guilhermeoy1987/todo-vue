<script setup>
const props = defineProps([
  'cadastraTarefa',
  'modelValue',
  'trocarFiltro'
])

const emits = defineEmits(['update:modelValue'])

const eventoInput = (evento) => {
  emits('update:modelValue', evento.target.value)
}
</script>

<template>
  <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input
          :value="modelValue"
          @input="eventoInput"
          required
          type="text"
          placeholder="Digite aqui sua tarefa"
          class="form-control"
        >
      </div>

      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">
          Adicionar Tarefa
        </button>
      </div>

      <div class="col-md-2">
        <select @change="trocarFiltro" class="form-control">
          <option value="todas">Todas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>