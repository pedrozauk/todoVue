<template>
  <div id="app" class="block">
    <h1 class="title">TODO LIST</h1>
    <span class="has-text-warning" v-if="editarA">Editando</span>
    <div class="todoarea box  is-flex is-flex-direction-column m-6 p-5">
      <input class="input pd-6 mb-5" type="text" name="inputTarefa" id="inputTarefa" v-model="inputTarefa">
      
      <button v-if="inputTarefa !=='' && editarA == false"  @click="adicionaTarefa" class="button is-primary" >Adicionar</button>
      <button v-if="editarA"  @click="editarTarefa" class="button is-warning" >Salvar</button>
 
  </div>
  <div id="arealista" class="" >
    
    <ul v-for="(tarefa, ind) in tarefas" :key="tarefa">
      <li class="message m-6 is-flex is-flex-direction-column ">
        <div class="message-header is-flex is-flex-direction-row-reverse is-align-content-flex-end">
          <div class="columns">
            <div class="column">
        <button class="button is-small has-background-warning" @click="sobeParaEdicao(ind)"  aria-label="delete">
          <span class="icon">
          <i class="fa has-text-black fa-edit"></i>
        </span>
        </button>
      </div>
      <div class="column">
        <button class="button is-small is-primary" @click="deletaTarefa(ind)">
        <span class="icon">
          <i class="fa fa-check has-text-black"></i>
        </span>
       </button>
      </div>
      </div>
       </div>
        <span class="p-5">{{ tarefa }}</span>
      
      </li>
    </ul>
  </div>

  </div>
</template>

<script>


//texss


export default {
    name: 'App',

    data(){
      return{
      inputTarefa:'',
      tarefas:[],
      editarA: false,
      idTarefaEditando:''
    }
    },
    mounted(){
      if(localStorage.getItem("tarefas")){
      this.tarefas = JSON.parse(localStorage.getItem("tarefas"));
      }
    },
    methods:{
      adicionaTarefa(){
        this.tarefas.push(this.inputTarefa);
        this.inputTarefa = '';
        this.salvaTarefas();
      },
      deletaTarefa(x){
        this.tarefas.splice(x,1);
        this.salvaTarefas();
  
      },
      salvaTarefas(){
        var parsed = JSON.stringify(this.tarefas);
        localStorage.setItem("tarefas",parsed);
      },
      sobeParaEdicao(x){
        this.editarA = true;
        this.inputTarefa = this.tarefas[x];
        this.idTarefaEditando = x

      },
      editarTarefa(){
        this.tarefas[this.idTarefaEditando] = this.inputTarefa;
        this.editarA = false;
        this.inputTarefa = '';
        this.salvaTarefas();
      }
     
    }
  
  }

  </script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
