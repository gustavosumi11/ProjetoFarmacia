<template>
    <div class="itens">
    <div class="float-right">
   
        <span class="abc">
         
            <table>
        <thead>
          <tr>
    
            <th class="columnType">Nome: {{ item.name }}</th>
            <th class="columnAmount">Valor: {{ item.value }}</th>
            
      
         
       
        <div class="icons">
            <i class="edit-item" @click="$emit('edit-item', item.id)"><b-icon icon="pencil" aria-hidden="true"></b-icon></i>

            <i class="delete-item" @click="$emit('del-iten-event', item.id)"><b-icon icon="trash-fill" aria-hidden="true"></b-icon>
            </i>
            </div>
        </tr>
        </thead>
     
    </table>
        </span>
    </div>
</div>
</template>

<script>
    export default {
        name: "ItemLista",
        props: ["item"]
    }
</script>

<style scoped>
    .glyphicon-pencil, .glyphicon-trash{
        font-size: 15px;
        padding: 4px;
    }
</style>
