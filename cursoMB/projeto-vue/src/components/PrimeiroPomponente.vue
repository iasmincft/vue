<template>
    <h1>titulo</h1>
</template>

<script>
    export default {
        name: 'PrimeiroPomponente',
        data() {
            return {
                mensagem: 'Olá, Vue!'
            }
        },
        methods: {
            exibirMensagem() {
                alert(this.mensagem);
            }
        }
    }
</script>