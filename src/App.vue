
<script setup>
import { reactive } from "vue";

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>

    <!--Formulário da descrição da tarefa-->
    <form @submit.prevent="cadastraTarefa"> <!--prevent -> a mesma coisa de e.preventDefault-->
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" required>
        </div>
        <!--Botão do formulário-->
        <div class="col-md-2">
          <button class="btn btn-primary">Cadastrar</button>
        </div>

        <!--Tipos de tarefas-->
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas as Tarefas</option>
            <option value="pendentes">Tarefas Pendentes</option>
            <option value="finalizadas">Tarefas Finalizadas</option>
          </select>      
        </div>
      </div>
    </form>

    <!--Tarefas (proriamente dito)-->
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>

.done {
  text-decoration: line-through;
}
</style>
