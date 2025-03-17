<template>
    <div :class="{'cliente': !isPremiun, 'cliente-premium': isPremiun}">
        <hr>
        <h4>Nome: {{ cliente.nome }}</h4>
        <hr>
        <p>Dscrição: {{ cliente.desc }}</p>
        <p>Número: {{ cliente.numero }}</p>
        <p>Email: {{ cliente.email }}</p>
        <p v-if=" showAge == true ">Idade: {{ cliente.idade }}</p>
        <p v-else>O usuario escondeu a idade</p>
        <button @click="mudarCor($event)">Mudar cor</button>
    </div>

    
</template>

<script>
export default {
    data(){
        return{
            isPremiun: false
        }
    },
    props: {
        cliente: Object,
        showAge: Boolean
    },
    methods: {
        mudarCor: function($event) {
            console.log($event)
            this.isPremiun = !this.isPremiun
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