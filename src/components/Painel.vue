<template>
    <draggable :list="painel" :disabled="!habilitado" class="list-group-panel" ghost-class="ghost" @start="arrastando = true"
            @end="arrastando = false" group="painel" >
        <transition type="transition" :name="!arrastando ? 'flip-list' : null">
            <div class="list-group-panel-item">
                <div slot="header" class="cabecalho">{{ titulo }}</div>
                <Caixa :tarefas="itens"/>
                <button @click.prevent="adicionar" class="botao">+</button>
            </div>
        </transition>
    </draggable>
</template>

<script>
    import Caixa from './Caixa'
    import draggable from 'vuedraggable'

    export default {
        name: 'Panel',
        components: { Caixa, draggable },
        data() {
            return { habilitado: true, arrastando: false }
        },
        props: {
            titulo: { type: String, required: true },
            itens: { type: Array, required: true },
            painel: { type: Array }
        },
        methods: {
            adicionar() {
                this.$emit('add')
            }
        }
    }
</script>

<style scoped>
    .painel {
        box-sizing: border-box;
        background-color: #efeff1;
        color: #000000;
        width: 300px;
        min-height: 40vh;
        padding: 15px;
        margin: 10px;
        float: left;
        border-radius: 5px;
    }

    .cabecalho {
        width: 100%;
        margin: 20px 5px;

    }

    .botao {
        width: 100%;
        background: transparent;
        height: 40px;
        text-align: center;
        border: none;
        font-size: 1.8rem;
        outline: none;
        cursor: pointer;
        margin-top: 10px;
    }
</style>