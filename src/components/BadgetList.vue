<template>
   <div class="badget-list-wrap">
      <el-card :header='header'>
         <template v-if="isItemList">
            <div class="bugest-list-item">
               <ListItem  v-for="(item, prop) in list" :key='prop' :item='item' @deleteItem='deleteItem'/>
            </div>
         </template>
         <template v-else>
            <el-alert type='info' :title='noList' :closable='false' />
         </template>
      </el-card>
   </div>
</template>



<script>
import ListItem from './BugetListItem.vue';

export default {
   components:{
      ListItem
   },
   name: 'BadgetList',
   props:{
      list:{
         type: Object,
         default: () =>({})
      }
   },
   data: ()=>({
      header: 'Список транзакций',
      noList: 'Список пустой'
   }),
   computed:{
      isItemList(){
         return Boolean(Object.keys(this.list).length);
      },
   },
   methods:{
      deleteItem(id){
         this.$emit('deleteItem',id)
      }
   }
}
</script>



<style scoped>
.badget-list-wrap{
   max-width: 500px;
   margin: 0 auto;
   text-align: center;
   font-weight: 700;
   font-size: 20px;
}
</style>