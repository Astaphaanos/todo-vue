
<script setup>
const props = defineProps(['cadastraTarefa', 'tarefatemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa"> <!--prevent -> a mesma coisa de e.preventDefault-->
      <div class="row">
        <div class="col">
          <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" required>
        </div>
        <!--Botão do formulário-->
        <div class="col-md-2">
          <button class="btn btn-primary">Cadastrar</button>
        </div>

        <!--Tipos de tarefas-->
        <div class="col-md-2">
          <select @change="props.trocarFiltro" class="form-control">
            <option value="todas">Todas as Tarefas</option>
            <option value="pendentes">Tarefas Pendentes</option>
            <option value="finalizadas">Tarefas Finalizadas</option>
          </select>      
        </div>
      </div>
    </form>
</template>