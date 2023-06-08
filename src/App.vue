<template>
  <div class="app">
  <div class="header">
    <Header />
  </div>
  <div id="listagem">
    
    <AddItem v-on:add-item-event="addItem" v-on:edit-item-event="editItemEvent" v-bind:editItem="editItem"/>
    <div>
      <Item v-bind:item="item" v-on:del-item-event="deleteItemFarma" v-on:edit-item-event="editItemFarma" />
    </div>
  </div>
</div>
</template>

<script>
  import Header from './components/header/header.vue'
  import Item from "./components/listagem/listagem.vue";
  import AddItem from "./components/listagem/listagemAdd.vue";

export default {
  name: 'App',
  components: {
    Item,
    AddItem,
    Header
  },
  data () {
    return {
      item: [],
      editItem: {
        name: '',
        id: ''
      }
    }
  },
  methods: {
    addItem(newitem){
      // console.log('newitem', newitem.name);
        this.item = [...this.item, newitem];
      // this.item.unshift(newitem)
    },
    deleteItemFarma(id){
      this.item = this.item.filter(item => item.id !== id);
    },
    editItemFarma(id){
      //find the index of the item's id
      let objIndex = this.item.findIndex(obj=> obj.id === id);
      this.editItem.name = this.item[objIndex].name;
      this.editItem.id = id;
    },
    editItemEvent(Item){
      //find the index of this id's object
      let objIndex = this.item.findIndex(obj => obj.id === Item.id)
      //update the item
      this.item[objIndex].name = Item.name;
    }
  },
  watch: {
    item: {
      handler() {
        localStorage.setItem('item',JSON.stringify(this.item))
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.getItem("item")){
      this.item = JSON.parse(localStorage.getItem("item"))
    }
  }
}
</script>

<style>
#listagem {
  margin-top: 10vh;
  text-align: center;
  color: #2c3e50;
 
}
</style>
