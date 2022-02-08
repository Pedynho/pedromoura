<template>
    <div class="question-title">Questão 1</div>
    <div class="question-title">Processamento de senha:</div>
    <div class="question-text">
        Crie funções de conferência para cada elemento necessário à entrada de senha
        (ao menos um caractere minúsculo, ao menos 8 caracteres, senhas iguais, etc...)
        e exiba os pontos conferidos apenas quando o usuário começar a digitar na caixa
        de texto.
    </div>

    <div class="form-group">
        <label for="senha"> <span> Senha: </span> </label>
        <input v-model="senha" type="password" id="senha" placeholder="Insira sua senha..." required/>

        <label for="senha"> <span> Repita a senha: </span> </label>
        <input v-model="senhaConf" type="password" id="senhaConf" placeholder="Repita a senha..." required/>
    </div>

    <span v-if="placeholder" class="senha-err">As duas senhas devem ser iguais!</span>

    <span v-if="placeholder" class="senha-err">
        <ul>
            <li :class="{'conferido': placeholder}">Pelo menos um caractere minúsculo</li>
            <li :class="{'conferido': placeholder}">Pelo menos um caractere maiúsculo</li>
            <li :class="{'conferido': placeholder}">Pelo menos um caractere especial</li>
            <li :class="{'conferido': placeholder}">Pelo menos um caractere numérico</li>
            <li :class="{'conferido': placeholder}">Pelo menos oito caracteres</li>
        </ul>
    </span>
</template>

<script>
    export default {
        name: "Senha",
        data() {
            return {
                senha: "",
                senhaConf: ""
            };
        },
        computed: {
            placeholder() {
                return true;
            }
        },
        methods: {}
    }
</script>

<style scoped>
 .form-group {
     display: grid;
     margin: 0 auto;
     grid-template-columns: auto 1fr;
     grid-template-rows: auto;
     grid-column-gap: 20px;
     grid-row-gap: 5px;
     width: 80%;
     margin-bottom: 5px;
 }

 @media query screen and (max-width: 800px) {
     .form-group {
         width: calc(100% - 20px);
     }
 }

 .form-group > label {
     display: flex;
     justify-content: center;
     align-content: center;
     flex-direction: column;
 }

 .form-group > label > span {
     width: 100%;
 }

 .form-group > input {
     border: 1px solid grey;
     border-radius: 5px;
 }

 .conferido {
     color: green !important;
 }

 .senha-err {
     color: red;
 }
</style>
