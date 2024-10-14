<script setup>
   const props = defineProps(['tarefasPendentes'])
</script>

<template>
  <header class="p-5 mb-4 mt-4 rounded-3 bg-light">
    <h1 class="fs-1">Olá</h1>
    <p>Você tem {{ props.tarefasPendentes }} tarefas pendentes</p>
  </header>
</template>
