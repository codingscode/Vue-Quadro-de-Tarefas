<template>
    <div id="app">
        <div v-for="(item, indice) in tarefas" :key="indice">
            <Painel :painel="tarefas" :titulo="item.titulo" :itens="item.itens" @add="adicionar(indice)" />
        </div>
    </div>
</template>

<script>
    import Painel from './components/Painel'

    let id = 1
    export default {
        name: 'app',
        components: {Painel},
        data () {
            return {
                habilitado: true,
                tarefas: [
                    {
                        titulo: 'Fazendo',
                        itens : [
                            { id: id++, titulo: 'Design UX Flows', categoria: 'purple', cor: ['purple'], usuarios: ['user-1.jpg', 'user-2.jpg'] },
                            { id: id++, titulo: 'Launch Website', categoria: 'yellow', cor: ['yellow', 'red'], usuarios: ['user-3.jpg'] },
                            { id: id++, titulo: 'Encontro de Cliente', categoria: 'red', cor: ['blue'], usuarios: ['user-2.jpg', 'user-4.jpg'] },
                            { id: id++, titulo: 'Lançar Build', categoria: 'blue', cor: ['green'], usuarios: ['user-4.jpg'] },
                            { id: id++, titulo: 'Desenvolver API', categoria: 'green', cor: ['purple'], usuarios: ['user-3.jpg', 'user-1.jpg'] }
                        ]
                    },
                    { titulo: 'Feito', itens: [] }
                ]
            }
        },
        methods: {
            adicionar(indice) {
                this.tarefas[indice].itens.push(
                    {id: id++, titulo: 'Final Tests', categoria: 'gray', cor: ['red'], usuarios: ['user-5.jpg', 'user-1.jpg']}
                )
            }
        }
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Roboto:300,400,700&display=swap');
    @import url('assets/css/reset.css');

    body {
        background-color: #5e74eb;
        font-family: 'Roboto', sans-serif;
        color: #ffffff;
    }

    #app {
        padding: 30px;
    }

    .list-group-panel-item {
        box-sizing: border-box;
        background-color: #efeff1;
        color: #000000;
        width: 300px;
        min-height: 40vh;
        padding: 15px;
        margin: 10px;
        float: left;
        border-radius: 5px;
        cursor: move;
    }

    .flip-list-move {
        transition: transform 1.5s;
    }

    .no-move {
        transition: transform 0s;
    }

    .fantasma {
        opacity: 0;
        background: #c8ebfb;
    }
</style>
