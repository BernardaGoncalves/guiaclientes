<template>

    <div id="app">
      <h1>Bem vindo ao Guia do Cliente</h1>
      <hr>
      <h2>Lista de Clientes</h2> <hr>

      <h3>Cadastro: </h3>
        <small class="avisoError" v-show="deuErro">Nome inválido! Tryy again</small><br>
        <input type="text" v-model="nomeField" placeholder="none"><br>
        <small class="avisoError" v-show="deuErro" >Email inválido! Tryy again</small><br>
        <input type="text" v-model="emailField" placeholder="email"><br>
        <small class="avisoError" v-show="deuErro" >Numero inválido! Tryy again</small><br>
        <input type="text" v-model="numeroField" placeholder="numero"><br>
        <small class="avisoError" v-show="deuErro" >Idade inválido! Tryy again</small><br>
        <input type="text" v-model="idadeField" placeholder="idade"><br>
        <small class="avisoError" v-show="deuErro" >Descricao inválido! Tryy again</small><br>
        <input type="text" v-model="descField" placeholder="descricao"><br>
        <button @click="cadastrarUser">Cadastrar</button>
      <hr>

      <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
        <h1>{{ index + 1 }}</h1>
        <ClienteList  :cliente="cliente" @meDelete= "deletaUser($event)" />
        
        <h4>Editar usuario</h4>
        <input type="text" v-model="cliente.nome">
        <input type="text" v-model="cliente.email">
        <input type="text" v-model="cliente.numero">
        <input type="text" v-model="cliente.idade">
        <input type="text" v-model="cliente.desc">
        <hr>

      </div>

      <ProdutoList/>
    </div>
</template>

<script>
import _ from 'lodash';
import ClienteList from './components/ClienteList.vue'
//import ProdutoList from './components/ProdutoList.vue';

export default {
  name: 'App',
  data() {
      return {
        deuErro: false,
        nomeField: "",
        emailField: "",
        numeroField: 0,
        idadeField: 0,
        descField: "",

        clientes: [
          {
        id: 8,
        nome: "Irene",
        email: "iris@gmail.com",
        numero: 23424,
        idade: 3,
        desc: "Coisa fofa"
          }
          ,
          {
          id: 7,
        nome: "Fanio",
        email: "Fan@gmail.com",
        numero: 7564,
        idade: 7,
        desc: "Best X9"
          },
          {
          id: 4,
          nome:"Ric",
          email:"ric@gmail.com",
          numero: 54435,
          desc: "Cool guy"
          },
          {
          id: 5,
          nome: "kinDog",
          email: "dog@gmail.com",
          numero: 7564,
          desc: "Dsycho dog"
          }
        ]
      }
    },
  components: {
    ClienteList,
    //ProdutoList
  },
  methods: {
    cadastrarUser: function() {
      if(this.nomeField == "" ||this.nomeField == "" || this.emailField == "" || this.numeroField == 0 || this.idadeField == 0 || this.descField == "" || this.nomeField < 3 ){
          this.deuErro = true
      } else {
        this.clientes.push({
        nome: this.nomeField,
        email: this.emailField,
        numero: this.numeroField,
        idade: this.idadeField,
        desc: this.descField,
        id: Date.now()
      })
        this.nomeField = ""
        this.emailField = ""
        this.numeroField = 0
        this.idadeField = 0
        this.descField = ""   

        this.deuErro = false
      }
      },
    deletaUser: function($event) {
      console.log("Evento Recebido")
      console.log($event)
      var id = $event.idDoCliente

      var novoArray = this.clientes.filter(cliente => cliente.id != id)

      this.clientes = novoArray

  }
  },
  computed: {
  //Ordenar a lista por ordem crescente
  orderClientes: function() {
    return _.orderBy(this.clientes,['nome'],['asc']);
  }
  }
}
</script>

<style>
  .avisoError{
    color: red;
  }

</style>
