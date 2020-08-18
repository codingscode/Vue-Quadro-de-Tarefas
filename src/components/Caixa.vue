<template>
    <div class="box">
        <draggable :list="tarefas" :disabled="!habilitado" class="grupo-lista" ghost-class="fantasma" @start="arrastando = true"
                @end="arrastando = false" group="box" >
            <transition-group type="transition" :name="!arrastando ? 'flip-list' : null">
                <div class="item-grupo-lista" v-for="elemento in tarefas" :key="elemento.id">
                    <div class="categoria" :style="{ backgroundColor: elemento.categoria }" />
                    <div class="content">
                        <div class="titulo">{{ elemento.titulo }}</div>
                        <div class="usuario">
                            <div v-for="(usuario, indice) in elemento.usuarios" :key="indice">
                                <img :src="require(`./../assets/images/${usuario}`)" :alt="usuario">
                            </div>
                        </div>
                        <div class="status">
                            <div v-for="(cor, indice) in elemento.cor" :key="indice" 
                                   :style="{ width: '30px', height: '10px', borderRadius: '5px', marginLeft: '5px', backgroundColor: cor}" />
                        </div>
                    </div>
                </div>
            </transition-group>
        </draggable>
    </div>
</template>

<script>
    import draggable from 'vuedraggable'

    export default {
        name: 'Box',
        components: { draggable },
        data() {
            return {
                habilitado: true,
                arrastando: false,
                item: [
                    { id: 100, titulo: "Desenvolvedor API", categoria: 'green', cor: ['purple'], usuarios: ['user-3.jpg', 'user-1.jpg']}
                ]
            };
        },
        props: {
            tarefas: { type: Array, required: true }
        }
    }
</script>

<style>

    .flip-list-move {
        transition: transform .2s;
    }

    .no-move {
        transition: transform 0s;
    }

    .fantasma {
        opacity: 0;
        background: #c8ebfb;
    }

    .grupo-lista {
        width: 100%;
        min-height: 200px;
        box-sizing: border-box;
    }

    .item-grupo-lista {
        max-width: 100%;
        height: 110px;
        box-sizing: border-box;
        background-color: #ffffff;
        margin: 10px 0;
        padding: 8px 8px 8px 12px;
        border-radius: 5px;
        cursor: move;
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }

    .categoria {
        content: "";
        min-width: 8px;
        height: 60px;
        margin-left: -12px;
        margin-right: 17px;
        border-radius: 0 5px 5px 0;
    }

    .item-grupo-lista i {
        cursor: pointer;
    }

    .titulo {
        font-size: 90%;
        margin: 8px 0;
    }

    .usuario {
        display: flex;
        flex-direction: row;
    }

    .usuario img {
        max-width: 35px;
        border-radius: 50%;
        margin-left: 5px;
    }

    .status {
        display: flex;
        flex-direction: row;
    }

</style>