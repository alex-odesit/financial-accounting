<template>
      <div class="list-item">
         <span class="budget-comment">{{item.comment}}</span>
         <span class="budget-value">{{item.value}}</span>
         <el-button type='danger' @click="deleteItem(item.id)">
            Удалить
         </el-button>
      </div>
</template>




<script lang="ts">
export default ({
   name: 'ListItem',
   props:{
      list:{
         type: Object,
         default: () =>({})
      },
      item:{
         type: Object,
         default: () =>({})
      },
   },
   methods:{
      deleteItem(id){
         this.$emit('deleteItem',id)
      }
   }

})
</script>





<style scoped>
.list-item{
   font-weight: 500;
   font-size: 16px;
   display: flex;
   text-align: center;
   padding: 10px 15px;
   align-items: center;
}
.budget-value{
   margin-left: auto;
   margin-right: 20px;
}
</style>