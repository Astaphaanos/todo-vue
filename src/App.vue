
<script setup>
import { reactive } from "vue";
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefa: [
    {
      titulo: "Estudar ES6",
      finalizada: false,
    },
    {
      titulo: 'Estudar Lógica de Programação',
      finalizada: false,
    },
    {
      titulo: 'Ir para academia',
      finalizada: true,
    },
    {
      titulo: 'Fazer prova de Programação Web',
      finalizada: false,
    }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefa.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefa.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado; //desestruturação {filtro}

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
      
    case 'finalizadas':
      return getTarefasFinalizadas();
      
    default:
      return estado.tarefa;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefa.push(tarefaNova);
  estado.tarefaTemp = '';
}


</script>

<template>
  <!--Header-->
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :tarefatemp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"
    :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value"/>
    <ListaDeTarefas :tarefa="getTarefasFiltradas()"/>
  </div>
</template>
