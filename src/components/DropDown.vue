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

    <div class="dropdown" :class="{'down': estado}"> {{ opcaoSelecionada }} ⬇ </div>
    <ul :class="{'opcoes': estado}">
        <!-- OPÇÕES PASSADAS (INDICANDO A ATUAL SELECIONADA) -->
    </ul>
</template>

<script>
    export default {
        name: "DropDown",
        props: {
            opcoesDD: Array
        },
        data() {
            return {
                opcaoSelecionada: "..."
            };
        },
        computed: {
            estado() { return true; }
        },
        methods: {
            // Permitir ler dados...
        },
        // Atualizar dados com opções passadas...
    }
</script>

<style scoped>
 .dropdown {
     cursor: pointer;
     border: 1px solid #2c3e50;
     border-radius: 5px;
     width: fit-content;
     padding: 5px;
 }

 .down {  }

 .opcoes {  }
</style>
