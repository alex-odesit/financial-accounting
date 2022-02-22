<template>
   <div class="total-value" :class="classSelect">
      Текущий баланс: {{total}}
   </div>
</template>


<script>
export default {
   name: 'TotalBalance',
   props: {
      total:{
         type: Number,
         default: 0
      },
      select:{
         type: String,
         default:''
      }
   },
   data:()=>({
      selectDef:'',
   }),
   computed:{
      classSelect(){
         if(this.select == 'INCOME'){
            return 'green'
         }
         else if(this.select == 'OUTCOME'){
            return 'red'
         }
         else return ''
      }
   }
}
</script>



<style scoped>
.total-value{
   font-size: 26px;
   text-transform: uppercase;
   padding: 20px;
   text-align: center;
}
.red{
   color: red;
}
.green{
   color: green;
}
</style>