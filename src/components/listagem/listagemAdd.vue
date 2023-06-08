<template>
    <div>
        <form @submit="addItem">
            <input type="text" name="name" v-model="name" placeholder="Inserir item">
            <input type="number" name="value" v-model="value" placeholder="Insira o valor">
                <input type="submit" value="Enviar" class="bot">
        </form>
    </div>
</template>

<script>
    export default {
        name: "AddItem",
        props: ['editItem'],
        data () {
            return {
                name: '',
                id: '',
                value: '',
                edit: false
            }
        },
        methods: {
            addItem(e){
                e.preventDefault();
                if (this.edit === false){
                    //Adiciona um novo Item
                    const novoItem = {
                        name: this.name,
                        value: this.value,
                        id: Math.floor(Math.random() * 100)
                    };
                    if (novoItem.name !== '' && novoItem.value !== ''){
                        this.$emit('add-item-event', novoItem);
                    }
                    this.name = ''
                    this.value = ''
                }else{
                    //edit item
                    const Item = {
                        name: this.name,
                        id: this.id,
                        value: this.value,
                    };
                    //send to parent (App.vue)
                    this.$emit('edit-item-event', Item);
                    // clear input field
                    this.name = '';
                    this.edit = false;
                    this.value = '';
                }
            }
        },
        watch: {
            editItem: {
                handler() {
                    this.name = this.editItem.name;
                    this.id = this.editItem.id;
                    this.edit = true
                    this.value= this.editItem.value;
                },
                deep: true
            },
            name:{
                handler(){
                    if(this.name === ''){
                        this.edit = false;
                    }
                }
            }
        }
    }
</script>

<style>
@import 'listagem.css'
</style>
