<script setup>
  const props = defineProps(['cadastraTarefa' , 'tarefaTemp', 'trocarFiltro' , 'editaTarefaTemp']);
</script>

<template>
  <form @submit.prevent="props.cadastraTarefa">
    <div class="row">
      <div class="col">
        <input
          :value="props.tarefaTemp"
          @change="props.editaTarefaTemp"
          required
          class="form-control"
          type="text"
          placeholder="Digite a tarefa desejada"
        />
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select
          @change="props.trocarFiltro"
          class="form-control"
        >
          <option value="todas">Todas as terefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
