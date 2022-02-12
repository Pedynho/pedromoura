<template>
    <div class="question-title">Questão 1</div>
    <div class="question-title">Processamento de senha:</div>
    <div class="question-text">
        Crie funções de conferência para cada elemento necessário à entrada de senha
        (ao menos um caractere minúsculo, ao menos 8 caracteres, senhas iguais, etc...)
        e exiba os pontos conferidos apenas quando o usuário começar a digitar na caixa
        de texto.
    </div>

    <div class="form-container">
        <div class="form-card">
            <div class="form-body">
                <div class="form-group">
                    <div class="input">
                        <input v-on:keyup="validation" v-model="senha" type="password" id="senha" placeholder="Insira sua senha..." required/>
                    </div>
                    <div class="input">
                        <input v-on:keyup="validation" v-model="senhaConf" type="password" id="senhaConf" placeholder="Repita a senha..." required/>
                    </div>
                </div>
                <div class="senha-err">
                    <ul>
                        <li :class="{'conferido': passValidation.lowcase}">Pelo menos um caractere minúsculo</li>
                        <li :class="{'conferido': passValidation.uppercase}">Pelo menos um caractere maiúsculo</li>
                        <li :class="{'conferido': passValidation.special}">Pelo menos um caractere especial</li>
                        <li :class="{'conferido': passValidation.number}">Pelo menos um caractere numérico</li>
                        <li :class="{'conferido': passValidation.eigthCh}">Pelo menos oito caracteres</li>
                    </ul>
                </div>
            </div>
            <div class="form-footer">
                <span v-if="!passValidation.equals" class="senha-err">As duas senhas devem ser iguais!</span>
            </div>
        </div>
    </div>


</template>

<script>
    export default {
        name: "Senha",
        data() {
            return {
                senha: "",
                senhaConf: "",
                passValidation: {
                    equals: true,
                    lowcase: false,
                    uppercase: false,
                    special: false,
                    number: false,
                    eigthCh: false,
                }
            };
        },
        methods: {
            validation() { 
                this.passValidation.eigthCh = this.senha.length >= 8
                this.passValidation.lowcase = this.senha.match(/[a-z]/g)            
                this.passValidation.uppercase = this.senha.match(/[A-Z]/g)
                this.passValidation.special = this.senha.match(/[^A-Za-z0-9]/g)           
                this.passValidation.number = this.senha.match(/[0-9]/g)
                this.passValidation.equals = this.senha === this.senhaConf          
            },
        },
    }
</script>

<style scoped>
    .form-container {
        display: flex;
        justify-content: center;
        align-content: center;
        padding: 2em;
    }
    .form-card {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        border-radius: 10px;
        border: 2px solid #ccc;
        box-shadow: 0 0 4px 3px rgba(0,0,0,0.12);
        padding: 10px;
    }
    .form-body{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        padding: 1em;
    }
    .input {
        padding: 5px;
    }
    .input input{
        font-size: 1em;
        outline: none;
        border: 0;
        height: 1.5em;
        border-bottom: 2px solid #ddb6f2;
    }
    .conferido {
        color: green !important;
    }

    .senha-err {
        font-size: 0.8em;
        color: red;
    }
</style>
