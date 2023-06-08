<template>
    <div>
        <h2>Lista de itens</h2>
        <div v-bind:key="item.id" v-for="item in item">
            <ItensFarma v-bind:item="item" v-on:del-iten-event="delItemMethod" v-on:edit-item="editItemMethod" />
        </div>
        <div v-if="!item.length">
            <p>Está vazio!</p>
        </div>
    </div>
</template>

<script>
    import ItensFarma from "./listagemItem.vue";
    export default {
        name: "ItensA",
        props: ["item"],
        components: {
            ItensFarma
        },
        methods: {
            delItemMethod(id){
               //Método para deletar item
                this.$emit('del-item-event', id);
            },
            editItemMethod(id){
                //Método para editar item
                this.$emit('edit-item-event', id)
            }
        }
    }
</script>

<style>
@import './listagem.css'
</style>
