<template>
  <form @submit.prevent="criarTarefa">
    <h1>Cadastro de Tarefa</h1>
    <div>
      <label for="titulo">Titulo</label>
      <input type="text" id="titulo" v-model="tarefa.titulo" />

      <label for="titulo">Status</label>
      <select id="status" v-model="tarefa.status">
        <option v-for="stat in status" :key="stat" :value="stat">
          {{ stat }}
        </option>
      </select>
    </div>
    <div>
      <label for="descricao">Descrição</label>
      <input type="textarea" id="descricao" v-model="tarefa.descricao" />
    </div>
    <button type="submit">Cadastrar</button>
  </form>
</template>

<script setup >
import axios from "axios";
import { ref, defineEmits } from "vue";

const status = ["aguardando", "fazendo", "finalizado"];

const emit = defineEmits(['tarefaAdicionada']);
const tarefa = ref({
  titulo: "",
  descricao: "",
  status: "",
});

const criarTarefa = () => {
  axios
    .post("http://127.0.0.1:8000/api/tarefas", tarefa.value)
    .then(() => {
      tarefa.value = {
        titulo: "",
        descricao: "",
        status: "",
      };
      emit('tarefaAdicionada')
      alert("Deu bom!")
    })
    .catch((erro) => {
      console.log(erro);
    });
};
</script>

<style>
</style>