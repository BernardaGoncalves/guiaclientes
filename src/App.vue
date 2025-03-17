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

      <div v-for="(cliente, index) in clientes" :key="cliente.id">
        <h1>{{ index }}</h1>
        <ClienteList  :cliente="cliente" :showAge="true"/>
        <hr>
        <h4>Editar</h4>
        <input type="text" v-model="cliente.nome">
        <input type="text" v-model="cliente.email">
        <input type="text" v-model="cliente.numero">
        <input type="text" v-model="cliente.idade">
        <input type="text" v-model="cliente.desc">

      </div>

      <hr>

      <h2>Lsta de Produtos</h2>

      <hr>
      <ProdutoList/>
    </div>
</template>

<script>

import ClienteList from './components/ClienteList.vue'
import ProdutoList from './components/ProdutoList.vue';

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
        nome: "saersfr",
        email: "zsregwr",
        numero: "sffffh",
        idade: 3,
        desc: "xfdgvfx"
          }
          ,
          {id: 7,
        nome: "saersfr",
        email: "zsregwr",
        numero: "sffffh",
        idade: 3,
        desc: "xfdgvfx"
          }
        ]
      }
    },
  components: {
    ClienteList,
    ProdutoList
  },
  methods: {
    cadastrarUser: function() {
      if(this.nomeField == "" ||this.nomeField == "" || this.emailField == "" || this.numeroField == 0 || this.idadeField == 0 || this.descField == ""   ){
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
      }
  }
}
</script>

<style>
  .avisoError{
    color: red;
  }

</style>
