<template>
    <div class="question-title">Questão 3</div>
    <div class="question-title">Edição de entradas:</div>
    <div class="question-text">
        Modifique este componente para que exiba as entradas da lista de objetos (com a estrutura abaixo) cujas as propriedades devem ser inputs no componente <tt>div.entrada</tt>, atualizando
        seus valores no componente pai caso editadas. Cada objeto na lista deve pertencer ao seu próprio elemento. Exiba todos corretamente, exiba os indicadores corretos e repasse os dados ao componente pai ao se clicar no botão atualizar.
        <br />
        <pre class="json-example"><i>// Entrada:</i>
<code>{
    id: Number,
    op1: String,
    op2: String
}</code></pre>
    </div>
    <div class="entradas-container">
        <div class="entradas">
            <div class="entrada" v-for="i in lista" :key="i.id">
                <div class="element-options" :id="i.id">
                    <span>Entrada Nº {{i.id}}</span>
                    <input type="text" v-model="i.op1" placeholder="Option 1">
                    <input type="text" v-model="i.op2" placeholder="Option 2">
                </div>
            </div>
            <button type="submit" @click="update" class="form-button">Atualizar</button>
        </div>
    </div>

    Indicadores:
    <ul>
        <li v-if="!lista">LISTA VAZIA</li>
        <li v-if="lista.length > 5">MAIS DE 5 ELEMENTOS</li>
        <li v-if="entradasValidas">UMA OU MAIS ENTRADAS NÃO RESPEITA O FORMATO</li>
    </ul>


</template>

<script>
    export default {
        name: "Lista",
        props: {
            dados: {
                type: Array,
                required: true
            }
        },
        data() {
            return {
                lista: this.$props.dados,
                placeholder: true,
            };
        },
        computed:{
            entradasValidas(){
                let validos = true
                this.lista.forEach((e) => {
                    if(e.op1.match(/[0-9]\.[0-9]/g) == null || e.op2.match(/[0-9]\.[0-9]/g) == null){
                        validos = false
                    }
                })
                return !validos
            }
        },
        methods: {
            update() {
                console.log(this.lista[1].op1)
                this.$emit("mudancaEmitida",this.lista)
            }
        }
    }
</script>

<style scoped>
 .form-button {
     font-size: 1.15rem;
     border-radius: 10px;
     border: 1px solid grey;
     background-color: #2c3e50;
     display: block;
     margin: 0 auto;
     padding: 5px;
     color: whitesmoke;
     cursor: pointer;
 }

.entradas{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 10px;
    border: 2px solid #ccc;
    box-shadow: 0 0 4px 3px rgba(0,0,0,0.12);
    padding: 10px;
    width: fit-content;
}

 .entradas-container {
    display: flex;
    justify-content: center;
    align-items: center;
 }

 .element-options{
    display: flex;
    flex-direction: column;
    padding: 10px;
 }
 .element-options input{
    margin: 5px;
    padding: 5px;
 }

 .json-example {
     font-style: normal;
     background-color: lightgrey;
     border: 1px solid #2c3e50;
     padding: 5px;
 }

 .json-example > code {
     font-family: "Courier New", monospace !important;
 }
</style>
