<template>
  <h1>Lista de tarefas</h1>
  <table>
    <thead>
        <tr>
            <td>Id: </td>
            <td>Titulo: </td>
            <td>Descricao: </td>
            <td>Status</td>
            <td></td>
        </tr>
    </thead>
    <tbody>
        <tr v-for="tarefa in tarefas" :key="tarefa.id">
            <td>{{ tarefa.id }}</td>
            <td>{{ tarefa.titulo }}</td>
            <td>{{ tarefa.descricao }}</td>
            <td>{{ tarefa.status }}</td>
            <td>
                <a href="#" @click="editarTarefa(tarefa.id)">Editar</a>
                <a href="#" @click="excluirTarefa(tarefa.id)">Excluir</a>
            </td>
        </tr>
    </tbody>
  </table>
</template>

<script setup>
import axios from 'axios';
import { defineProps } from 'vue';

defineProps({
    tarefas: Array,
})

const emit = defineEmits(['tarefaExcluida'])

const excluirTarefa = (id) => {
    axios.delete(`http://127.0.0.1:8000/api/tarefas/${id}`)
    .then(()=>{
        alert('Tarefa excluida');
        emit('tarefaExcluida');
    })
}

const editarTarefa = () => {
    
}
</script>

<style>
</style>