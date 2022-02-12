<template>
    <div class="question-title">Questão 2</div>
    <div class="question-title">Dropdown:</div>
    <div class="question-text">
        Transforme a estrutura dada em um seletor dropdown (como um <tt>&#60;select/&#62;</tt>)
        a partir das opções dadas em <tt>:opcoesDD</tt>, indicando a opção atualmente selecionada
        no texto do seletor e visualmente na lista de opções. A opção padrão deve ser inicialmente
        a primeira opção dada na lista. Crie também uma função que retorne a opção selecionada no
        formato <tt>[ texto, idx ]</tt> ('texto' sendo a opção em si, e 'idx' seu índice na lista)
        para leitura pelo componente pai.
    </div>
    <div class="dropdown-container">
        <div class="dropdown-body">
            <div @click="showOptions" class="dropdown"> {{ opcaoSelecionada }} ⬇ </div>
            <div v-if="listOptions" class="list-options">
                <ul class="options">
                    <li  v-for="(option, i) in opcoesDD" :key="i" @click="choseOption(i)" :class="{'selected': option === this.opcaoSelecionada}">{{option}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "DropDown",
        props: {
            opcoesDD: Array
        },
        data() {
            return {
                listOptions: false,
                opcaoSelecionada: this.$props.opcoesDD[0]
            };
        },
        methods: {
            showOptions(){
                this.listOptions = !this.listOptions

            },
            choseOption(i){
                this.opcaoSelecionada = this.$props.opcoesDD[i]
                this.$emit("opSelected",[this.opcaoSelecionada, i])
                this.listOptions = !this.listOptions
            }
        },
        // Atualizar dados com opções passadas...
    }
</script>

<style scoped>
    .dropdown-container{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 2em;
    }
    .dropdown-body{
        cursor: pointer;
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-content: center;
        border-radius: 10px;
        border: 2px solid #ccc;
        box-shadow: 0 0 4px 3px rgba(0,0,0,0.12);
        padding: 10px;
        width: fit-content;
    }
    .list-options{
        position: absolute;
        top: 100%;
        left: 0;
        background-color: white;
        border-radius: 10px;
        border: 2px solid #ccc;
        box-shadow: 0 0 4px 3px rgba(0,0,0,0.12);
        width: 100%;
    }
    .dropdown{
        padding: 5px;
    }
    .options{
        list-style-type: none;
        padding: 0;
        margin: 0;
    }
    .options li {
        padding: 5px;
    }
    .selected {
        background-color: lightskyblue;
        border-radius: 5px;
    }
</style>
