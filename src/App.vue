<template>
  <div id="app" class="block">
    <div class="todoarea box  is-flex is-flex-direction-column m-6 p-5">
      <input class="input pd-6 mb-5" type="text" name="inputTarefa" id="inputTarefa" v-model="inputTarefa">
    <button @click="adicionaTarefa" class="button is-primary">Adicionar</button>
  </div>
  <div id="arealista" class="" >
    <ul v-for="(tarefa, ind) in tarefas" :key="tarefa">
      <li class="message m-6 is-flex is-flex-direction-column">
        
        <span class="p-5">{{ tarefa }}</span>
       <button class="button is-danger" @click="deletaTarefa(ind)">
        Feito
       </button>
      </li>
    </ul>
  </div>
  </div>
</template>

<script>
export default {
    name: 'App',
    data(){
      return{
      inputTarefa:'',
      tarefas:[]}
    },
    mounted(){
      if(localStorage.getItem("tarefas")){
      this.tarefas = JSON.parse(localStorage.getItem("tarefas"));
      }
    },
    methods:{
      adicionaTarefa(){
        this.tarefas.push(this.inputTarefa);
        this.salvaTarefas();
      },
      deletaTarefa(x){
        this.tarefas.splice(x,1);
        this.salvaTarefas;
  
      },
      salvaTarefas(){
        var parsed = JSON.stringify(this.tarefas);
        localStorage.setItem("tarefas",parsed);
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
