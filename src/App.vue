<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro : 'Todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo : 'Estudar ES6',
        finalizada : false
      },
      {
        titulo : 'Estudar CSS',
        finalizada : false
      },
      {
        titulo : 'Ir a academia',
        finalizada : true
      },

    ]
  })

  const getPendingTasks = () => {
   return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
  }

  const getFinalizedTasks = () => {
   return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
  }

  const getAllTasks = () => {
   return estado.tarefas
  }

  const getFilteredTasks = () => {
    const filtro = estado.filtro;

    switch (filtro) {
      case 'pendentes': return getPendingTasks();
      case 'finalizadas': return getFinalizedTasks();
      default : return getAllTasks();
    }
  }
  const registerTask = () => {
    const newTask = {
      titulo: estado.tarefaTemp,
      finalizada :false,
    }
    estado.tarefas.push(newTask);
    estado.tarefaTemp = ''
  }

</script>

<template>
  <div class="container">

  <header class="p-5 mb-4 mt-4 rounded-3 bg-light">
    <h1 class="fs-1">Olá</h1>
    <p>
      Você tem {{ getPendingTasks().length }} tarefas pendentes
    </p>
  </header>

<form  @submit.prevent="registerTask()">
  <div class="row">
    <div class="col">
      <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required class="form-control" type="text" placeholder="Digite a tarefa desejada">
    </div>
    <div class="col-md-2">
      <button class="btn btn-primary" type="submit">Cadastrar</button>
    </div>
    <div class="col-md-2">
      <select @change="evento => estado.filtro = evento.target.value" class="form-control">
        <option value="todas">Todas as terefas</option>
        <option value="pendentes">Tarefas pendentes</option>
        <option value="finalizadas">Tarefas finalizadas </option>
      </select>
    </div>
  </div>
</form>
<ul class="list-group mt-4">
  <li class="list-group-item" v-for="tarefa in getFilteredTasks()">
    <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
    <label :class="{done: tarefa.finalizada === true}" class="ms-3" :for="tarefa.titulo">
      {{ tarefa.titulo }}
    </label>
  </li>
</ul>

</div>
</template>

<style scoped>

.done{
  text-decoration: line-through;
}
</style>
