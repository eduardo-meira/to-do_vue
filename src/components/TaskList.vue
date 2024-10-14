<script setup>
  const props = defineProps(['tarefas'])
</script>

<template>
  <ul  class="list-group mt-4">
    <p class="fs-3 text-center mt-5"  v-if="tarefas >= 0">Não existe tarefas pendentes</p>
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input
        @change="(evento) => (tarefa.finalizada = evento.target.checked)"
        :checked="tarefa.finalizada"
        :id="tarefa.titulo"
        type="checkbox"
      />  
      <label
        :class="{ done: tarefa.finalizada === true }"
        class="ms-3"
        :for="tarefa.titulo"
      >
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</template>
