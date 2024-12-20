
<template>
  <CadastrarTarefa @tarefaAdicionada="getTarefas"></CadastrarTarefa>
  <Tarefas :tarefas="tarefas" @tarefaExcluida="getTarefas"></Tarefas>
</template>

<script setup>
import axios from "axios";
import Tarefas from "./components/Tarefas.vue";
import CadastrarTarefa from "./components/CadastrarTarefa.vue";
import { ref } from "vue";

const tarefas = ref([])

const getTarefas = () => {
  axios.get("http://127.0.0.1:8000/api/tarefas").then((response) => {
    tarefas.value = response.data;
  });
};

getTarefas();
</script>
<style scoped>
</style>
