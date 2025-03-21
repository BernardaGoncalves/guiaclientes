<template>
    <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
        <hr>
        <h4>Nome: {{ cliente.nome }}</h4>
        <hr>
        <p>Dscrição: {{ cliente.desc }}</p>
        <p>Número: {{ cliente.numero }}</p>
        <p>Email: {{  processEmail }}</p>
        <p v-if=" showAge == true ">Idade: {{ cliente.idade }}</p>
        <p v-else>O usuario escondeu a idade</p>
        <button @click="mudarCor($event)">Mudar cor</button>
        <button @click="emitirEventDelet">Deletar</button>
        <h4>Id especial: {{ idEspecial }}</h4>
    </div>

    
</template>

<script>
export default {
    data(){
        return{
            isPremium: false
        }
    },
    props: {
        cliente: Object,
        showAge: Boolean
    },
    methods: {
        mudarCor: function($event) {
            console.log($event)
            this.isPremiun = !this.isPremium
        },
        emitirEventDelet: function() {
            console.log("Emitindo do filho")
            this.$emit("meDelete", {idDoCliente: this.cliente.id, curso: "Node.js", promocao: true, component: this})

        }
    },
    computed: {
        processEmail: function(){
            return this.cliente.email.toUpperCase()
        },
        idEspecial: function(){
            return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase()
        }
    }

}
</script>

<style scoped>
    .cliente{
        max-width: 600px;
        max-height: 600px;
        padding: 2%;
        margin-bottom: 4%;
        background-color: antiquewhite;
    }
    .cliente-premium{
        max-width: 600px;
        max-height: 600px-;
        padding: 2%;
        background-color:black;
        margin-bottom: 4%;
        color: yellow;
    }

</style>