<script setup>
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import TaskList from "./components/TaskList.vue";

const estado = reactive({
  filtro: "Todas",
  tarefaTemp: "",
  tarefas: [
    {
      titulo: "Estudar ES6",
      finalizada: false,
    },
    {
      titulo: "Estudar CSS",
      finalizada: false,
    },
    {
      titulo: "Ir a academia",
      finalizada: true,
    },
  ],
});

const getPendingTasks = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada === false);
};

const getFinalizedTasks = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada === true);
};

const getAllTasks = () => {
  return estado.tarefas;
};

const getFilteredTasks = () => {
  const filtro = estado.filtro;

  switch (filtro) {
    case "pendentes":
      return getPendingTasks();
    case "finalizadas":
      return getFinalizedTasks();
    default:
      return getAllTasks();
  }
};
const registerTask = () => {
  const newTask = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };
  estado.tarefas.push(newTask);
  estado.tarefaTemp = "";
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getPendingTasks().length" />
    <Formulario :tarefa-temp="estado.tarefaTemp"
     :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"
     :cadastra-tarefa="registerTask"
     :trocar-filtro="evento => estado.filtro = evento.target.value"/>  
    <TaskList :tarefas="getFilteredTasks()"/>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
