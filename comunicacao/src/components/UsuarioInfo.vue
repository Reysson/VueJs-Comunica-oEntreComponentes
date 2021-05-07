<template>
    <div class="componente">
        <h2>As Informações de Usuário</h2>
        <p>Nome do usuário: {{ inverteNome() }}</p>
        <button @click="reiniciarNome">Reiniciar nome</button>
        <p>Idade do infame {{idade}}</p>
    </div>
</template>

<script>
import barramento from '@/barramento'
export default {
    props: {
        nome:{
            type: String,
            required : true
        },
        idade:{
            type: Number,
            required : false
        }
    },
    methods:{
        inverteNome(){
            return this.nome.split('').reverse().join('')
        },
        reiniciarNome(){
            this.nome = 'Maria'
            this.$emit('nomeMudou',this.nome) //dispara evento
        }
    },
    created(){
        barramento.quandoIdadeMudar(parametro =>{ //escuta evento do componente irmão
            this.idade = parametro
        })
    }
}
</script>

<style scoped>
    .componente {
        flex: 1;
        background-color: #ec485f;
        color: #fff;
    }
</style>
